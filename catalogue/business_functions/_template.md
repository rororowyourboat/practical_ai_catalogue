# Business Function: [Function Name]

## Overview
[One-paragraph description of the function and why AI is relevant]

## AI-Applicable Tasks

### Task 1: [Task Name]

**FCTAF Complexity Profile:**
- **Synthesis Depth**: [Unimodal / Multi-hop / Deep Synthesis]
- **Epistemic Friction**: [Structured / Semi-structured / Entropic]
- **Intent Variance**: [Convergent / Guided / Divergent]

**Pipeline Architecture:**
| Stage | Node Type | Edge to Next | Failure Risk | Notes |
|---|---|---|---|---|
| I. Intent Framing | [Human/AI/Code] | [Deterministic/Dynamic/Feedback] | Low/Med/High | [why] |
| II. Epistemic Mapping | [Human/AI/Code] | [Deterministic/Dynamic/Feedback] | Low/Med/High | [which sources] |
| III. Info Retrieval | [Human/AI/Code] | [Deterministic/Dynamic/Feedback] | Low/Med/High | [data quality] |
| IV. Logical Synthesis | [Human/AI/Code] | [Deterministic/Dynamic/Feedback] | Low/Med/High | [reasoning type] |
| V. Transduction | [Human/AI/Code] | [Deterministic/Dynamic/Feedback] | Low/Med/High | [output format] |

**Feedback Loops:**
- [e.g., IV → III: Grounding verification (unverified claims trigger re-retrieval)]
- [e.g., V → V: Schema validation (format errors trigger re-generation)]
- Exit conditions: [what terminates each loop]

**Predicted Primary Failure Point:** [Stage N — reason]
**Symptomatic Stage:** [where it would show up]
**Root Cause Diagnostic:** [node type + edge type that enables propagation]

**Optimization Strategy:**
- [e.g., "Dynamic edge I → II → add scope contract (deterministic edge)"]
- [e.g., "AI Node at Stage IV → add Human review gate or feedback edge to III"]
- [e.g., "High Epistemic Friction → hybrid search + reranking at Stage III"]

**Success Metrics:**
| Stage | Metric | Target |
|---|---|---|
| I | Task Acceptance Rate | [target] |
| II | Source Relevance Rate | [target] |
| III | Precision / Recall / F1 | [target] |
| IV | Faithfulness Score | [target] |
| V | Schema Conformance Rate | [target] |

**Maturity**: ★★★☆☆

**Tools/Providers**: [tool links]

**Cost Estimate**: [rough pricing per unit]

**Limitations**: [failure modes, edge cases]

**Human Oversight**: [None / Light / Heavy / Full HITL] — driven by Intent Variance + Node assignments

---

### Task 2: [Task Name]
...

## Function Summary

**Node distribution across tasks:**
- Code Nodes: [count]
- AI Nodes: [count]
- Human Nodes: [count]

**Edge risk profile:**
- Deterministic edges: [count] (low propagation risk)
- Dynamic edges: [count] (high propagation risk — candidates for contract enforcement)
- Feedback edges: [count] (need exit conditions)

**Most common primary failure stage:** [Stage N — reason]
**Most common symptomatic stage:** [Stage N — what people notice]

## Case Studies / Examples
- [Example 1]: Link or description
- [Example 2]: Link or description

## Gaps & Opportunities
- [Gap 1]: Missing tooling or capability
- [Opportunity 1]: Emerging approach
