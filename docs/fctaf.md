# Functional Cognitive Task-Analytic Framework (FCTAF)

## 1. Abstract

The FCTAF provides a structured foundation for classifying AI-applied business tasks by decomposing them into five distinct operational stages. Unlike traditional hierarchies (e.g., Bloom's Taxonomy), which categorize by the "quality" of thought, this framework categorizes by the **computational and epistemic demands** of each stage. This enables precise identification of failure modes in both AI and human workflows, and maps directly to architecture decisions and optimization strategies.

**Prior Art & Influences:**
- NIST AI Risk Management Framework — operational task categorization
- Stanford HAI — AI capability assessment dimensions
- Sarker (2022) — multi-dimensional task classification
- Bloom's Taxonomy — cognitive demand levels
- Fleishman's Ability Taxonomy — deductive reasoning abilities
- Information Foraging Theory — epistemic friction and search behavior

## 2. The 5-Stage Task Supply Chain

Every task is viewed as a "supply chain" of information processing. A breakdown at any stage results in an incomplete or incorrect outcome.

| Stage | Operational Process | Academic Correlate | Primary AI Bottleneck |
|---|---|---|---|
| **I. Intent Framing** | Goal definition, scope identification, constraint setting | Metacognition | **Ambiguity Drift**: Failure to narrow down the problem space |
| **II. Epistemic Mapping** | Selecting the correct knowledge base, tools, and data sources | Cognitive Architecture (Sensing) | **Tool-Use Blindness**: Looking in the wrong "room" for data |
| **III. Info Retrieval** | Targeted extraction of specific, verified data points from selected sources | Selective Attention / RAG | **Precision Fatigue**: Overlooking "needles" in high-noise haystacks |
| **IV. Logical Synthesis** | Connecting disparate data points via multi-step (multi-hop) reasoning | System 2 Thinking / Chain-of-Thought | **Hallucination**: Inventing logical links between valid data points |
| **V. Transduction** | Mapping the synthesized result into the target format/syntax | Semiotic Mapping | **Schema Violation**: Right information, wrong delivery shape |

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

## 3. Dimensions of Complexity (Difficulty Levers)

To determine the "risk" or "effort" of a task, evaluate it along three continuous levers. These form the **Task Complexity Profile**.

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

## 4. Diagnostic Mapping: Predicting Failure Points

By overlaying the Pipeline Stages with the Complexity Levers, we can predict where a task will fail and what optimization to apply.

| Task Profile | High-Difficulty Stage | Expected Failure | Optimization Strategy |
|---|---|---|---|
| Open-ended goal | Stage I (Framing) | Wrong solution path | Iterative scoping, clarification prompts |
| Messy documents | Stage III (Retrieval) | Missing information | Vector search, reranking, hybrid retrieval |
| Complex logic | Stage IV (Synthesis) | Logical fallacies | Chain-of-Thought, multi-agent verification |
| Strict output format | Stage V (Transduction) | Format/syntax errors | Few-shot prompting, structured output, JSON mode |
| Wrong data source | Stage II (Mapping) | Irrelevant or stale answers | Router agents, metadata filtering, source selection |
| High ambiguity + high stakes | Stage I + IV | Scope creep + hallucination | Human-in-the-loop at framing + synthesis gates |

## 5. Evaluative Metrics (Per-Stage Success Measurement)

To measure whether an AI system is actually working at each stage:

| Stage | Metric | How to Measure |
|---|---|---|
| I. Intent Framing | **Task Acceptance Rate** | % of tasks where the AI's interpretation matches user intent (validated by user feedback or gold-standard framing) |
| II. Epistemic Mapping | **Source Relevance Rate** | % of queries routed to the correct knowledge base / tool (measured via ground-truth source labels) |
| III. Info Retrieval | **Precision / Recall / F1** | Standard IR metrics: of all retrieved chunks, how many are relevant? Of all relevant chunks, how many were retrieved? |
| IV. Logical Synthesis | **Faithfulness Score** | % of synthesized claims that are grounded in retrieved evidence (no hallucinated links). Use attribution / citation checking. |
| V. Transduction | **Schema Conformance Rate** | % of outputs that pass validation (JSON schema, format spec, length constraints, tone guidelines) |

**Composite Metric:** Weight each stage's score by its difficulty contribution to get an overall **Task Reliability Score**. A task with high Epistemic Friction weights Stage III heavier; a task with deep Synthesis Depth weights Stage IV heavier.

## 6. Relationship to Prior Framework

FCTAF subsumes and extends the initial 4-dimension classification:

| Original Dimension | FCTAF Integration |
|---|---|
| Epistemic Demand | Maps to **Stages I, IV** (framing complexity + synthesis depth) |
| Data Grounding | Maps to **Stages II, III** (source selection + retrieval quality) + **Epistemic Friction** lever |
| Operational Objective | Maps to **Stage V** (what the output action is) |
| Degree of Determinism | Maps to **Intent Variance** lever (convergent → divergent) |

The original dimensions are retained as **descriptive tags**. FCTAF adds the **diagnostic pipeline** that explains *why* a task is hard and *where* it will break.

## 7. Forward-Looking Use Cases

**For Product Managers:** Use the 5-stage pipeline + 3 levers to determine if a feature needs a simple LLM call or a complex RAG + agentic workflow. A task with low Epistemic Friction and low Synthesis Depth is a single API call. High on both = multi-agent system.

**For Engineers:** Use the diagnostic map to decide where to invest engineering effort. If Stage III is the bottleneck, don't spend time on a better model — build better retrieval. If Stage I is the bottleneck, improve task design and user intent capture.

**For Business Leaders:** Use the Task Complexity Profile to estimate project risk and cost. Tasks that fail at Stage I or II are organizational problems, not AI problems.

**For Researchers:** Use FCTAF to benchmark models at specific stages (e.g., "A benchmark specifically for Stage IV multi-hop reasoning with entropic sources").

## 8. Open Questions

- [ ] How do the 3 levers interact? Is difficulty additive, multiplicative, or does it depend on the task?
- [ ] Can we assign numerical ranges to each lever (e.g., Synthesis Depth 1-5) to produce a composite difficulty score?
- [ ] How does model size/capability shift the difficulty curve? (Does a bigger model reduce effective Synthesis Depth?)
- [ ] Are there task profiles where the diagnostic map doesn't apply or is misleading?
- [ ] How does FCTAF apply to multi-modal tasks (text + image + audio) — does each modality have its own pipeline?
