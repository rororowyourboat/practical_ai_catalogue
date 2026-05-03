# Research Plan: Practical AI Catalogue

## Overall Context
Catalogue how current multimodal AI can be applied to real business problems. Uses the **Functional Cognitive Task-Analytic Framework (FCTAF)** — a diagnostic framework that decomposes every task into a 5-stage information supply chain, profiled by 3 complexity levers. This enables businesses to predict failure points, select architectures, and measure success at each stage.

**Full framework documentation:** [docs/fctaf.md](docs/fctaf.md)

## Theoretical Framework (FCTAF)

### The 5-Stage Task Supply Chain
Every AI task is a pipeline. A breakdown at any stage produces a wrong outcome.

| Stage | Process | Bottleneck |
|---|---|---|
| I. Intent Framing | Goal definition, scoping, constraint setting | Ambiguity Drift |
| II. Epistemic Mapping | Selecting correct knowledge bases and tools | Tool-Use Blindness |
| III. Info Retrieval | Extracting verified data from selected sources | Precision Fatigue |
| IV. Logical Synthesis | Multi-hop reasoning across data points | Hallucination |
| V. Transduction | Formatting output to target schema/tone | Schema Violation |

### 3 Complexity Levers (Task Difficulty Profile)
| Lever | Low | High |
|---|---|---|
| **Synthesis Depth** | Unimodal (1 hop) | Deep Synthesis (5+ hops) |
| **Epistemic Friction** | Structured (clean SQL) | Entropic (messy PDFs) |
| **Intent Variance** | Convergent (1 answer) | Divergent (many valid answers) |

### Diagnostic Map
| Profile | Failure Point | Fix |
|---|---|---|
| Open-ended goal | Stage I | Iterative scoping |
| Messy documents | Stage III | Vector search / reranking |
| Complex logic | Stage IV | Chain-of-Thought / multi-agent |
| Strict output format | Stage V | Few-shot / structured output |
| Wrong data source | Stage II | Router agents / source selection |

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
- [ ] Define business function taxonomy
- [ ] Map business functions to FCTAF profiles
- [ ] Inventory tools with per-stage capability ratings

## Current Hypotheses
1. **H1 — Multimodal AI is production-ready for more tasks than businesses assume**: Most businesses only use text LLMs; vision, audio, and agentic workflows are underutilized.
2. **H2 — Stage I and II failures explain most "AI didn't work" outcomes**: The bottleneck isn't model capability — it's intent framing and source selection. Businesses deploy AI at Stage III+ without investing in Stages I-II.
3. **H3 — Commodity tooling exists for 80% of common use cases**: Open-source + API solutions cover most needs; custom training is rarely required.
4. **H4 — Intent Variance predicts deployment success**: Convergent tasks (deterministic) are automatable; divergent tasks (probabilistic) need human-in-the-loop. The mismatch between task variance and deployment expectations causes failures.
5. **H5 — Epistemic Friction is the hidden cost driver**: Structured tasks cost 10x less than entropic tasks with similar Synthesis Depth, because pre-processing (Stage III) dominates engineering effort.

## Phase 1: Framework Deepening
- [x] Repository initialized
- [x] FCTAF framework documented (5 stages + 3 levers + diagnostic map + metrics)
- [ ] Deep-dive each stage (failure taxonomy, techniques, tooling, benchmarks)
- [ ] Quantify the 3 levers (numerical ranges, composite scoring)
- [ ] Test framework against real-world business tasks for validity

## Phase 2: Business Function Mapping
- [ ] Define business function taxonomy (sales, marketing, ops, support, finance, HR, product, legal)
- [ ] Profile each function's common AI tasks on FCTAF dimensions
- [ ] Identify high-value, low-friction opportunities per function
- [ ] Create catalogue entries with full pipeline + lever profiles

## Phase 3: Tool Inventory & Architecture Patterns
- [ ] Survey current multimodal AI tools and providers
- [ ] Rate tools by which pipeline stages they excel at
- [ ] Document architecture patterns per FCTAF profile
- [ ] Build cost estimates tied to complexity profile

## Phase 4: Case Studies & Validation
- [ ] Select 3-5 real business use cases
- [ ] Apply FCTAF analysis → predict failure points
- [ ] Build and measure against per-stage metrics
- [ ] Validate/refine framework based on results

## Done Work
- [x] Repository initialized with git
- [x] Initial 4-dimension classification (NIST/HAI/Sarker 2022)
- [x] FCTAF framework synthesized and documented
- [x] Plan, journal, catalogue templates, and index updated
