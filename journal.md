# Research Journal: Practical AI Catalogue

## 2026-05-03 14:16 — Project Kickoff

**Hypothesis**: Multimodal AI is production-ready for more business tasks than most organizations realize, and integration complexity — not model capability — is the real bottleneck.

**Reasoning**: Most businesses interact with AI through chat interfaces (text-only). Meanwhile, vision models can read invoices, speech models handle customer calls, and agentic frameworks automate multi-step workflows — yet adoption remains low outside tech-first companies.

**Expectations**: We'll find that 60-70% of common business tasks have at least one production-ready AI solution, but most require custom integration work that keeps adoption limited to companies with engineering teams.

**Research Plan**:
- [ ] Define business function taxonomy
- [ ] Map AI modalities to functions
- [ ] Inventory current tools/providers
- [ ] Evaluate maturity and feasibility

**Findings**:
[To be filled as research progresses]

**Conclusions**:
[To be filled]

---

## 2026-05-03 14:30 — Framework Evolution: 4 Dimensions → FCTAF v1

**Hypothesis**: A descriptive classification (what kind of task) is insufficient — we need a diagnostic framework (where does it break, how do we fix it).

**Reasoning**: The initial 4-dimension model (Epistemic Demand, Data Grounding, Operational Objective, Degree of Determinism) from NIST/HAI/Sarker 2022 was good at *describing* tasks but didn't explain *why* tasks fail or *what to build*. By restructuring as a 5-stage pipeline with 3 complexity levers, we can predict failure points, map failures to optimization strategies, and measure success at each stage independently.

**Key Insight**: Most "AI project failures" happen at Stage I (Intent Framing) and Stage II (Epistemic Mapping) — before the model even runs. Businesses deploy AI at Stage III+ without investing in problem definition and source selection.

**Decisions**:
- FCTAF subsumes the original 4 dimensions (they map to specific stages/levers)
- Added per-stage evaluative metrics
- Restructured plan into 4 phases: Framework Deepening → Business Mapping → Tool Inventory → Case Studies

**Next Steps**:
- [ ] Deep-dive each FCTAF stage individually
- [ ] Begin business function taxonomy

---

## 2026-05-03 14:50 — Framework Evolution: FCTAF v1 → v2

**Hypothesis**: A pipeline model without actors and edges can locate where a failure occurs, but cannot diagnose *who caused it* or *how it spread*.

**Reasoning**: v1 identified the stage but had three gaps:
1. No actor model — no way to distinguish whether a Code, AI, or Human failure character was responsible
2. No edge model — no way to distinguish whether a failure propagated silently (dynamic edge) or was caught (deterministic edge)
3. Linear assumption — real pipelines have feedback loops, retries, and backtracking

**Key Insights**:
- **Upstream failures present as downstream symptoms.** A Stage II failure (wrong source) looks like a Stage III failure (bad retrieval). Without tracing edges and nodes, you treat the symptom instead of the cause.
- **Dynamic edges are the primary propagation vector.** They allow malformed outputs to pass undetected. Replacing dynamic edges with deterministic ones (output contracts) is the single highest-leverage intervention.
- **Feedback loops need exit conditions.** A loop without an exit condition is an unmodeled failure mode — this explains most runaway agent behavior in production.
- **Node type determines failure character.** Code fails loudly (traceable), AI fails silently (plausible), Human fails inconsistently (variable). This determines your diagnostic approach.

**New Hypothesis (H6)**: Dynamic edges are the primary failure propagation vector. Most production AI failures are symptomatic, not primary. Replacing dynamic edges with deterministic edges (output contracts) would eliminate the majority of silent failures.

**Decisions**:
- Added Node Taxonomy (Code / AI / Human) with failure characters and selection heuristics
- Added Edge Taxonomy (Deterministic / Dynamic / Feedback) with propagation risk
- Added formal diagnostic procedure (5 steps: symptom → edge → trace back → node → feedback check)
- Added feedback loop patterns with re-entry points, delta signals, and exit conditions
- Added edge-level metrics (Contract Pass Rate, Interpretation Accuracy, Loop Convergence Rate)
- Added worked example with full pipeline architecture + diagnostic walk-through
- Updated all templates with node/edge columns and feedback loop documentation

**Open Questions for v3**:
- Stage output contracts (formal schema for what "passing" looks like at each boundary)
- Multi-agent handoffs mid-stage (sub-pipelines vs. node composition)
- Confidence propagation (should each stage output carry a confidence score?)
- Numerical lever ranges and composite scoring
- Lever interaction effects
- Model size effects on difficulty curve

**Next Steps**:
- [ ] Deep-dive each stage with node/edge considerations
- [ ] Formalize stage output contracts
- [ ] Begin business function taxonomy
