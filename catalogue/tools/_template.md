# Tool Category: [Category Name]

## Overview
[One-paragraph description of the tool category]

## FCTAF Stage Affinity

Which pipeline stages this category of tools primarily addresses:

| Stage | Affinity | Notes |
|---|---|---|
| I. Intent Framing | Low/Med/High | [why] |
| II. Epistemic Mapping | Low/Med/High | [why] |
| III. Info Retrieval | Low/Med/High | [why] |
| IV. Logical Synthesis | Low/Med/High | [why] |
| V. Transduction | Low/Med/High | [why] |

## Node Type Support

| Node Type | Supported? | Notes |
|---|---|---|
| Code Node (deterministic) | Yes/No | [e.g., structured output, JSON mode, function calling] |
| AI Node (probabilistic) | Yes/No | [e.g., open-ended generation, reasoning] |
| Human Node (assisted) | Yes/No | [e.g., review UIs, approval workflows, HITL interfaces] |

## Complexity Sweet Spots

| Lever | Best Performance | Degradation Point |
|---|---|---|
| Synthesis Depth | [e.g., up to 2-hop] | [e.g., 3+ hops degrades] |
| Epistemic Friction | [e.g., structured → semi-structured] | [e.g., entropic sources] |
| Intent Variance | [e.g., convergent tasks] | [e.g., highly divergent goals] |

## Edge Support

| Edge Type | Supported? | Notes |
|---|---|---|
| Deterministic (output contracts) | Yes/No | [e.g., JSON schema validation, type guarantees] |
| Dynamic (open handoff) | Yes/No | [e.g., natural language context passing] |
| Feedback (loop support) | Yes/No | [e.g., retry logic, re-generation, refinement] |

## IR Design Space Profile
*Technical dimensions mapped to [[../information_retreival/10_Design_Space]]*

| Dimension | Implementation | DS Ref |
|---|---|---|
| **Data Landscape** | [Unstructured / Semi / Structured] | [[06]] |
| **Query Landscape** | [Fact / Procedural / Analytical / Contextual] | [[07]] |
| **Representation** | [Sparse / Dense / Hybrid / Graph] | [[08]] |
| **Retrieval Engine** | [Lexical / Semantic / Hybrid / Generative] | [[09]] |
| **Reranking Tier** | [None / Cross-Encoder / LLM-Reranker] | [[10]] |
| **Context Strategy** | [Naive / Semantic Chunking / Optimization] | [[13/14]] |
| **Agentic Loop** | [None / Dynamic / Feedback] | [[15/22]] |

## Tools

### [Tool Name]
- **Provider**: [Company/Org]
- **URL**: [link]
- **API**: [REST / SDK / CLI / Chat]
- **Pricing**: [model]
- **FCTAF Profile**: [Stages, Node Types, Complexity Levers]
- **IR Design Profile**: [Representation, Retrieval, Reranking, Loop]
- **Key Strengths**: [bullet list]
- **Limitations**: [bullet list]
- **Best For**: [specific use case patterns]

### [Tool Name]
...

## Comparison Matrix

| Tool | Price | Stage Coverage | Node Types | Edge Types | Max Depth | Friction Tolerance | Notes |
|---|---|---|---|---|---|---|---|
| [Tool] | [$] | III, IV, V | AI, Code | Det, Dyn | 3-hop | Semi-structured | [note] |
