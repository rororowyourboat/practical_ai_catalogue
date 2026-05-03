# Functional Cognitive Task-Analytic Framework (FCTAF) — v2

## 1. What Changed and Why

Version 1 established a five-stage supply chain model for classifying tasks by their computational and epistemic demands. It was useful for pre-mortem planning but had three gaps that limited its diagnostic value:

- **No actor model.** It described what happens to information but not who or what is responsible at each stage.
- **No edge model.** It treated stages as isolated boxes with no formal model of how outputs pass between them — or how failures travel downstream.
- **Linear assumption.** Real pipelines retry, backtrack, and re-enter at earlier stages. This was unmodeled.

v2 addresses all three by integrating a node taxonomy and edge taxonomy borrowed from workflow graph theory. The result is a framework that can diagnose not just *where* a failure occurred, but *what type of actor caused it* and *how the failure propagated*.

---

## 2. The 5-Stage Pipeline (Unchanged from v1)

Each stage represents a distinct epistemic operation. A failure at any stage produces an incorrect or incomplete output, which may or may not be detectable at that stage.

| Stage | Operation | AI Failure Mode |
|---|---|---|
| **I. Intent Framing** | Goal definition, scope, and constraint setting | Ambiguity Drift |
| **II. Epistemic Mapping** | Selecting the correct knowledge source or environment | Tool-Use Blindness |
| **III. Info Retrieval** | Targeted extraction of verified data from the selected source | Precision Fatigue |
| **IV. Logical Synthesis** | Multi-step reasoning across retrieved data points | Hallucination |
| **V. Transduction** | Mapping synthesized output to the required format or consumer | Schema / Semantic Violation |

### Stage Deep-Dives

#### Stage I: Intent Framing
The system must understand *what* the user actually wants — not just the literal request, but the underlying goal, constraints, and success criteria. Most "AI project failures" happen here: the task was framed too broadly, too narrowly, or against the wrong objective.

**Examples:**
- "Summarize this quarterly report" → Ambiguity: Which metrics matter? Audience level? Desired length?
- "Answer customer questions about returns" → Scope: Which products? Which jurisdictions? Policy version?

**Engineering Implication:** This stage is often solved by **human design**, not AI. Good prompt engineering, system prompts, and task scoping are Stage I interventions.

#### Stage II: Epistemic Mapping
Given a well-framed intent, the system must select *where* to look. This includes choosing knowledge bases, APIs, databases, or tools. Wrong mapping means the system solves the right problem with the wrong data.

**Examples:**
- Tax question routed to general training data instead of current tax code database
- Customer query routed to product docs instead of order history

**Engineering Implication:** Router agents, intent classifiers, and tool-selection logic. This is where RAG system design matters most.

#### Stage III: Info Retrieval
Given the right source, extract the right data points. This is where vector search quality, chunking strategy, and retrieval precision matter.

**Examples:**
- Finding the specific clause in a 200-page contract
- Pulling the correct SKU from a messy inventory spreadsheet

**Engineering Implication:** Embedding quality, chunking strategies, reranking, hybrid search (keyword + semantic), query decomposition.

#### Stage IV: Logical Synthesis
Given correct data points, reason to the correct conclusion. This is the classic "reasoning" challenge — multi-hop inference, causal chains, contradiction resolution.

**Examples:**
- "Is this contract compliant with GDPR?" requires connecting multiple clauses across sections
- "What caused the Q3 revenue drop?" requires correlating multiple data streams

**Engineering Implication:** Chain-of-thought prompting, multi-agent debate, structured decomposition, symbolic verification layers.

#### Stage V: Transduction
Given a correct conclusion, deliver it in the right shape. The information is right but the format is wrong — wrong schema, wrong tone, wrong level of detail.

**Examples:**
- Correct answer but not in the required JSON schema
- Accurate analysis but written for engineers when the audience is executives

**Engineering Implication:** Few-shot prompting, output parsers, structured output modes (JSON mode), tone/style instructions.

---

## 3. Node Taxonomy — Who Owns Each Stage

Every stage in a pipeline is executed by one of three actor types. The actor type determines the *character* of the failure when that stage breaks down.

| Node Type | Description | Failure Character |
|---|---|---|
| **Code Node** | Deterministic, rule-based execution. No contextual judgment. | Fails loudly and precisely. Errors are traceable. |
| **AI Node** | LLM or ML model handling contextual, probabilistic reasoning. | Fails silently or plausibly. Errors may look like valid output. |
| **Human Node** | Human judgment, creativity, or domain expertise. | Fails inconsistently. Errors depend on attention, expertise, and fatigue. |

### Stage-to-Node Assignment

Stages do not have a fixed node type. The assignment is a *design decision* that carries tradeoffs.

| Stage | Typical Node Assignment | Risk of Mis-assignment |
|---|---|---|
| I. Intent Framing | Human or AI | Assigning to Code locks in scope prematurely |
| II. Epistemic Mapping | AI or Code | Assigning to AI risks Tool-Use Blindness at scale |
| III. Info Retrieval | Code or AI | Assigning to Human introduces inconsistency and bottleneck |
| IV. Logical Synthesis | AI (with Human review) | Assigning to Code alone fails on novel reasoning; AI alone risks Hallucination |
| V. Transduction | Code or AI | Assigning to Human is the most common over-reliance point |

### Node Selection Heuristics

**Choose Code Node when:**
- The task is deterministic with clear input/output contracts
- Errors must be traceable and loud
- The operation is high-volume and must be consistent

**Choose AI Node when:**
- The task requires contextual interpretation or judgment
- The input is ambiguous or unstructured
- Multiple valid outputs exist (Intent Variance is high)

**Choose Human Node when:**
- The task requires domain expertise not captured in training data
- The cost of silent failure is unacceptably high
- The task is one-off or low-volume, making automation unjustifiable

---

## 4. Edge Taxonomy — How Stages Connect

Edges define the transition between stages. They determine whether a failure at one stage is detectable before it propagates to the next.

| Edge Type | Description | Failure Propagation Risk |
|---|---|---|
| **Deterministic Edge** | Fixed, rule-based handoff. Output format and validity are checkable. | Low. Failures are caught at the boundary. |
| **Dynamic Edge** | Context-dependent handoff. The receiving stage must interpret what it receives. | High. A malformed input may be accepted and acted on silently. |
| **Feedback Edge** | Output is routed back to an earlier stage for revision. | Variable. Reduces primary failure risk but can create loops without exit conditions. |

### The Propagation Problem

A key diagnostic insight: **upstream failures often present as downstream symptoms.**

A Stage II failure (wrong knowledge source selected) will produce empty or irrelevant output at Stage III. An observer watching only Stage III sees a retrieval failure. The root cause is one stage earlier. This is the *upstream failure / symptomatic failure* distinction:

- **Primary failure:** The stage where the root cause originates.
- **Symptomatic failure:** The stage where the error becomes visible in the output.

Dynamic edges increase the gap between primary and symptomatic failure because they allow malformed outputs to pass undetected. Deterministic edges reduce this gap because they enforce output contracts at the boundary.

### Edge Design Heuristics

**Use Deterministic Edges when:**
- The output format is known and checkable (JSON schema, type system, validation rules)
- Downstream stages cannot recover from malformed input
- You want to minimize the gap between primary and symptomatic failure

**Use Dynamic Edges when:**
- The output is inherently open-ended or context-dependent
- The receiving stage is an AI Node capable of interpreting variable input
- The cost of over-constraining the handoff exceeds the cost of occasional misinterpretation

**Use Feedback Edges when:**
- The downstream stage can detect quality issues in its own output
- Re-processing with additional context can improve the result
- You need iterative refinement (but always define an exit condition)

---

## 5. Complexity Levers (Unchanged from v1)

These three dimensions define the difficulty profile of a task and predict which stages are most at risk.

### A. Synthesis Depth (The "Hop" Count)
How many reasoning steps connect the input to the output?

- **Unimodal**: Direct answer from one data point (1 hop)
- **Multi-hop**: Requires synthesizing data from multiple sources or logical steps (2-4 hops)
- **Deep Synthesis**: Complex chains with branching, backtracking, or constraint satisfaction (5+ hops)

*Prior Art: Fleishman's Deductive Reasoning abilities*

**Architecture Mapping:**
| Depth | Architecture |
|---|---|
| Unimodal | Single API call |
| Multi-hop | RAG pipeline + CoT |
| Deep Synthesis | Multi-agent + structured decomposition |

### B. Epistemic Friction (Source Messiness)
How messy, noisy, or contradictory are the input sources?

- **Structured**: Clean, predictable format (SQL, REST API, well-formed JSON)
- **Semi-structured**: Partially predictable (Markdown, HTML tables, forms)
- **Entropic**: Unstructured, noisy, or contradictory (handwritten notes, diverse PDFs, multi-language sources)

*Prior Art: Information Foraging Theory*

**Architecture Mapping:**
| Friction Level | Pre-Processing Required |
|---|---|
| Structured | Direct input, no pre-processing |
| Semi-structured | Light parsing (HTML → text, table extraction) |
| Entropic | Heavy pre-processing (OCR, normalization, deduplication, entity resolution) |

### C. Intent Variance (The "Ambiguity" Index)
How many valid solutions exist?

- **Convergent**: One correct path and answer (deterministic) — "Convert this to JSON"
- **Guided**: Few valid paths, clear constraints — "Summarize this to 3 bullet points"
- **Divergent**: Many valid strategies and outcomes (probabilistic) — "Draft a marketing strategy"

*Prior Art: Bloom's "Evaluate" and "Create" levels*

**Architecture Mapping:**
| Variance | Human Oversight Required |
|---|---|
| Convergent | Automatable with confidence thresholds |
| Guided | Light review (spot-check) |
| Divergent | Heavy review (human-in-the-loop) |

---

## 6. Diagnostic Mapping — v2

Combining stages, node types, and edge types produces a richer failure diagnosis.

| Observed Symptom | Likely Primary Failure | Node to Inspect | Edge to Inspect |
|---|---|---|---|
| Wrong solution path | Stage I — Intent Framing | Human or AI Node | Dynamic edge from I → II (no scope contract enforced) |
| Missing or irrelevant information | Stage II — Epistemic Mapping | AI or Code Node | Deterministic edge absent between II → III |
| Correct source, wrong data extracted | Stage III — Info Retrieval | AI Node | Dynamic edge accepting low-confidence outputs |
| Plausible but logically invalid output | Stage IV — Logical Synthesis | AI Node | No feedback edge back to III for grounding |
| Correct reasoning, wrong output shape | Stage V — Transduction | Code or AI Node | No output contract enforced at pipeline exit |

### Diagnostic Procedure

1. **Identify the symptomatic stage** — where does the error become visible?
2. **Check the incoming edge** — is it deterministic (failure should have been caught) or dynamic (failure propagated silently)?
3. **Trace back one stage** — inspect the primary failure candidate
4. **Check node type** — Code nodes fail loudly (likely caught), AI nodes fail silently (likely propagated), Human nodes fail inconsistently (intermittent)
5. **Check for missing feedback edge** — could a feedback loop have caught this before it became symptomatic?

---

## 7. The Feedback Loop as a First-Class Element

v1 modeled tasks as linear pipelines. In practice, most non-trivial pipelines include at least one feedback edge. v2 treats feedback loops as a required design element, not an exception.

A well-designed feedback loop requires three things:

- **A re-entry point:** Which stage does the pipeline return to?
- **A delta signal:** What information is passed back to inform the revision?
- **An exit condition:** What criterion terminates the loop?

Feedback loops without exit conditions are the most common cause of runaway agent behavior in production systems. A loop that re-enters Stage I indefinitely without a convergence criterion is not a feature — it is an unmodeled failure mode.

### Feedback Loop Patterns

| Pattern | Re-entry Point | Delta Signal | Exit Condition |
|---|---|---|---|
| **Retrieval Refinement** | Stage III | "Missing: [specific data gap]" + revised query | F1 score above threshold, or max retries |
| **Grounding Verification** | Stage III from IV | "Unverified claim: [claim text]" + source request | All claims have ≥1 supporting citation |
| **Scope Clarification** | Stage I from IV | "Ambiguous intent: [specific ambiguity]" + clarification question | User confirms scope, or max clarifications |
| **Output Validation** | Stage V from V | "Schema violation: [field, error]" + correction prompt | Output passes validation, or max retries |

---

## 8. Task Complexity Profile — Worked Example

To illustrate the framework in use, consider an automated research and insights pipeline.

**Task:** Given a research brief, collect market data, synthesize findings, and produce a stakeholder report.

| Stage | Node Type | Edge to Next Stage | Complexity Lever at Risk |
|---|---|---|---|
| I. Intent Framing | Human Node | Dynamic → II | High Intent Variance. Scope is ambiguous until human commits. |
| II. Epistemic Mapping | AI Node | Deterministic → III | Moderate Epistemic Friction. Source selection must be validated before retrieval begins. |
| III. Info Retrieval | Code Node | Dynamic → IV | High Epistemic Friction. Data quality varies across sources. |
| IV. Logical Synthesis | AI Node + Human review | Feedback → III or IV | High Synthesis Depth. Multi-hop reasoning across heterogeneous sources. |
| V. Transduction | Code Node | Deterministic → output | Low. Format is fixed (report template). |

**Predicted failure points:**
- Stage II (AI selects wrong source category) presenting as Stage III symptom (retrieval returns irrelevant data)
- Stage IV (hallucinated logical link) if feedback edge back to Stage III is absent
- Stage I → II dynamic edge: if scope contract is not enforced, ambiguous intent propagates silently through the entire pipeline

**Diagnostic walk-through:**
If a stakeholder reports "the report's conclusions don't follow from the data":
1. Symptomatic stage: IV (Logical Synthesis) — conclusions are wrong
2. Incoming edge: Dynamic from III → IV (could have passed bad data)
3. Trace back: Is Stage III data correct? If yes → primary failure is IV (hallucination). If no → primary failure is II (wrong source) presenting as III (bad retrieval)
4. Node check: Stage IV is AI Node → silent failure likely (hallucinated links look plausible)
5. Missing feedback: No grounding feedback edge from IV → III → add one

---

## 9. Per-Stage Evaluative Metrics

| Stage | Metric | How to Measure |
|---|---|---|
| I. Intent Framing | **Task Acceptance Rate** | % of tasks where the AI's interpretation matches user intent (validated by user feedback or gold-standard framing) |
| II. Epistemic Mapping | **Source Relevance Rate** | % of queries routed to the correct knowledge base / tool (measured via ground-truth source labels) |
| III. Info Retrieval | **Precision / Recall / F1** | Standard IR metrics: of all retrieved chunks, how many are relevant? Of all relevant chunks, how many were retrieved? |
| IV. Logical Synthesis | **Faithfulness Score** | % of synthesized claims that are grounded in retrieved evidence (no hallucinated links). Use attribution / citation checking. |
| V. Transduction | **Schema Conformance Rate** | % of outputs that pass validation (JSON schema, format spec, length constraints, tone guidelines) |

### Edge-Level Metrics

| Edge Type | Metric | How to Measure |
|---|---|---|
| Deterministic | **Contract Pass Rate** | % of handoffs that pass the validation gate |
| Dynamic | **Interpretation Accuracy** | % of handoffs where the receiving stage correctly interprets the sender's intent |
| Feedback | **Loop Convergence Rate** | % of feedback loops that terminate within N iterations (vs. hitting max retries) |

### Composite Scoring

Weight each stage's score by its difficulty contribution to get an overall **Task Reliability Score**. A task with high Epistemic Friction weights Stage III heavier; a task with deep Synthesis Depth weights Stage IV heavier.

---

## 10. Relationship to v1 Framework

| v1 Dimension | v2 Integration |
|---|---|
| Epistemic Demand | Maps to **Stages I, IV** (framing complexity + synthesis depth) |
| Data Grounding | Maps to **Stages II, III** (source selection + retrieval quality) + **Epistemic Friction** lever |
| Operational Objective | Maps to **Stage V** (what the output action is) |
| Degree of Determinism | Maps to **Intent Variance** lever (convergent → divergent) |
| *(new)* Actor Model | **Node Taxonomy** (Code / AI / Human) at each stage |
| *(new)* Edge Model | **Edge Taxonomy** (Deterministic / Dynamic / Feedback) between stages |
| *(new)* Failure Propagation | **Primary vs. Symptomatic Failure** distinction + diagnostic procedure |

The v1 dimensions are retained as **descriptive tags**. v2 adds the **diagnostic pipeline** (actors, edges, propagation) that explains *why* a task fails, *who* caused it, and *how* it spread.

---

## 11. Forward-Looking Use Cases

**For pipeline diagnosis:** Use the Diagnostic Mapping table (Section 6) to distinguish primary from symptomatic failures. Start by identifying the observed symptom, then trace back through node types and edge contracts to find the root stage.

**For pipeline design:** Use the Stage-to-Node Assignment table (Section 3) to make deliberate actor decisions. Every dynamic edge is a risk you are accepting. Every deterministic edge is a contract you are enforcing. Every feedback edge needs an exit condition.

**For benchmarking:** Isolate a single stage, fix the node type, and measure failure rate against a controlled input set. This enables stage-specific model evaluation rather than end-to-end accuracy, which conflates failure sources.

**For business leaders:** Use the Task Complexity Profile to estimate project risk and cost. Tasks that fail at Stage I or II are organizational problems, not AI problems. Tasks that fail at Stage III or IV are engineering problems. Tasks that fail at Stage V are integration problems.

---

## 12. Open Questions for v3

- **Evaluative Metrics:** How do you measure whether a stage succeeded? What does a passing stage-boundary output look like, formally? Can we define a schema for each stage's output contract?
- **Multi-agent handoffs:** When a Human Node delegates to an AI Node mid-stage (rather than between stages), how is that modeled? Is this a sub-pipeline or a node composition?
- **Confidence propagation:** Should each stage output carry a confidence score that downstream stages can use to decide whether to accept or trigger a feedback loop?
- **Numerical lever ranges:** Can we assign numerical ranges to each lever (e.g., Synthesis Depth 1-5) to produce a composite difficulty score?
- **Lever interactions:** How do the 3 levers interact? Is difficulty additive, multiplicative, or does it depend on the task profile?
- **Model size effects:** How does model size/capability shift the difficulty curve? Does a bigger model reduce effective Synthesis Depth?
- **Multi-modal pipelines:** How does FCTAF apply to multi-modal tasks (text + image + audio) — does each modality have its own sub-pipeline?
