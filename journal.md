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

## 2026-05-03 14:30 — Framework Evolution: 4 Dimensions → FCTAF

**Hypothesis**: A descriptive classification (what kind of task) is insufficient — we need a diagnostic framework (where does it break, how do we fix it).

**Reasoning**: The initial 4-dimension model (Epistemic Demand, Data Grounding, Operational Objective, Degree of Determinism) from NIST/HAI/Sarker 2022 was good at *describing* tasks but didn't explain *why* tasks fail or *what to build*. By restructuring as a 5-stage pipeline with 3 complexity levers, we can:
1. Predict failure points before building
2. Map failures to specific optimization strategies
3. Measure success at each stage independently

**Key Insight**: Most "AI project failures" happen at Stage I (Intent Framing) and Stage II (Epistemic Mapping) — before the model even runs. Businesses deploy AI at Stage III+ without investing in problem definition and source selection.

**Decisions**:
- FCTAF subsumes the original 4 dimensions (they map to specific stages/levers)
- Added H5: Epistemic Friction is the hidden cost driver
- Added per-stage evaluative metrics (Task Acceptance Rate, Source Relevance, P/R/F1, Faithfulness, Schema Conformance)
- Restructured plan into 4 phases: Framework Deepening → Business Mapping → Tool Inventory → Case Studies

**Next Steps**:
- [ ] Deep-dive each FCTAF stage individually
- [ ] Quantify the 3 levers with numerical ranges
- [ ] Begin business function taxonomy
