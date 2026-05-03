# Research Plan: Practical AI Catalogue

## Overall Context
Catalogue how current multimodal AI can be applied to real business problems. Uses the **Functional Cognitive Task-Analytic Framework (FCTAF v2)** — a diagnostic framework that decomposes every task into a 5-stage information supply chain with actor types (nodes), connection types (edges), and 3 complexity levers. This enables businesses to predict failure points, trace root causes, select architectures, and measure success at each stage.

**Full framework documentation:** [docs/fctaf.md](docs/fctaf.md)

## Theoretical Framework (FCTAF v2)

### The 5-Stage Task Supply Chain
Every AI task is a pipeline. A breakdown at any stage produces a wrong outcome.

| Stage | Process | Bottleneck |
|---|---|---|
| I. Intent Framing | Goal definition, scoping, constraint setting | Ambiguity Drift |
| II. Epistemic Mapping | Selecting correct knowledge bases and tools | Tool-Use Blindness |
| III. Info Retrieval | Extracting verified data from selected sources | Precision Fatigue |
| IV. Logical Synthesis | Multi-hop reasoning across data points | Hallucination |
| V. Transduction | Formatting output to target schema/tone | Schema Violation |

### Node Taxonomy (Who Owns Each Stage)
| Node Type | Failure Character |
|---|---|
| **Code Node** | Fails loudly and precisely. Errors are traceable. |
| **AI Node** | Fails silently or plausibly. Errors look like valid output. |
| **Human Node** | Fails inconsistently. Depends on attention, expertise, fatigue. |

### Edge Taxonomy (How Stages Connect)
| Edge Type | Propagation Risk |
|---|---|
| **Deterministic Edge** | Low — failures caught at the boundary |
| **Dynamic Edge** | High — malformed input accepted silently |
| **Feedback Edge** | Variable — reduces primary risk but needs exit conditions |

### Key Diagnostic Insight
**Upstream failures present as downstream symptoms.** A Stage II failure (wrong source) looks like a Stage III failure (bad retrieval). Trace back through node types and edge contracts to find the primary failure.

### 3 Complexity Levers (Task Difficulty Profile)
| Lever | Low | High |
|---|---|---|
| **Synthesis Depth** | Unimodal (1 hop) | Deep Synthesis (5+ hops) |
| **Epistemic Friction** | Structured (clean SQL) | Entropic (messy PDFs) |
| **Intent Variance** | Convergent (1 answer) | Divergent (many valid answers) |

### Per-Stage Evaluative Metrics
| Stage | Metric |
|---|---|
| I. Intent Framing | Task Acceptance Rate |
| II. Epistemic Mapping | Source Relevance Rate |
| III. Info Retrieval | Precision / Recall / F1 |
| IV. Logical Synthesis | Faithfulness Score |
| V. Transduction | Schema Conformance Rate |

## Current Work To-Dos
- [ ] Deepen FCTAF Stage I (Intent Framing) — techniques, patterns, failure taxonomy
- [ ] Deepen FCTAF Stage II (Epistemic Mapping) — source selection architectures
- [ ] Deepen FCTAF Stage III (Info Retrieval) — retrieval strategies and benchmarks
- [ ] Deepen FCTAF Stage IV (Logical Synthesis) — reasoning architectures and limits
- [ ] Deepen FCTAF Stage V (Transduction) — structured output and format engineering
- [ ] Formalize output contracts per stage (schema for stage boundary validation)
- [ ] Investigate confidence propagation between stages
- [ ] Define business function taxonomy
- [ ] Map business functions to FCTAF profiles
- [ ] Inventory tools with per-stage capability ratings

## Current Hypotheses
1. **H1 — Multimodal AI is production-ready for more tasks than businesses assume**: Most businesses only use text LLMs; vision, audio, and agentic workflows are underutilized.
2. **H2 — Stage I and II failures explain most "AI didn't work" outcomes**: The bottleneck isn't model capability — it's intent framing and source selection. Businesses deploy AI at Stage III+ without investing in Stages I-II.
3. **H3 — Commodity tooling exists for 80% of common use cases**: Open-source + API solutions cover most needs; custom training is rarely required.
4. **H4 — Intent Variance predicts deployment success**: Convergent tasks (deterministic) are automatable; divergent tasks (probabilistic) need human-in-the-loop.
5. **H5 — Epistemic Friction is the hidden cost driver**: Structured tasks cost 10x less than entropic tasks with similar Synthesis Depth, because pre-processing (Stage III) dominates engineering effort.
6. **H6 — Dynamic edges are the primary failure propagation vector**: Most production AI failures are not root-cause failures — they are symptomatic failures caused by dynamic edges allowing upstream errors to pass undetected. Replacing dynamic edges with deterministic edges (output contracts) would eliminate the majority of silent failures.

## Phase 1: Framework Deepening
- [x] Repository initialized
- [x] FCTAF v1 documented (5 stages + 3 levers + diagnostic map + metrics)
- [x] FCTAF v2 documented (added node taxonomy, edge taxonomy, feedback loops, diagnostic procedure, edge-level metrics)
- [ ] Deep-dive each stage (failure taxonomy, techniques, tooling, benchmarks)
- [ ] Formalize stage output contracts (what a passing boundary looks like)
- [ ] Investigate confidence propagation between stages
- [ ] Quantify the 3 levers (numerical ranges, composite scoring)
- [ ] Test framework against real-world business tasks for validity

## Phase 2: Business Function Mapping
- [ ] Define business function taxonomy (sales, marketing, ops, support, finance, HR, product, legal)
- [ ] Profile each function's common AI tasks on FCTAF v2 dimensions (stages + nodes + edges + levers)
- [ ] Identify high-value, low-friction opportunities per function
- [ ] Create catalogue entries with full pipeline + lever profiles

## Phase 3: Tool Inventory & Architecture Patterns
- [ ] Survey current multimodal AI tools and providers
- [ ] Rate tools by which pipeline stages they excel at
- [ ] Document architecture patterns per FCTAF profile (including node/edge design)
- [ ] Build cost estimates tied to complexity profile

## Phase 4: Case Studies & Validation
- [ ] Select 3-5 real business use cases
- [ ] Apply FCTAF analysis → predict failure points, node assignments, edge types
- [ ] Build and measure against per-stage and per-edge metrics
- [ ] Validate/refine framework based on results

## Done Work
- [x] Repository initialized with git
- [x] Initial 4-dimension classification (NIST/HAI/Sarker 2022)
- [x] FCTAF v1 framework synthesized and documented
- [x] FCTAF v2: added node taxonomy, edge taxonomy, feedback loops, diagnostic procedure
- [x] Plan, journal, catalogue templates, and index updated
