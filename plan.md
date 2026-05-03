# Research Plan: Practical AI Catalogue

## Overall Context
Catalogue how current multimodal AI can be applied to real business problems. Uses a multi-dimensional task classification framework (adapted from NIST, Stanford HAI, Sarker 2022) to map every use case along four axes — enabling businesses to assess feasibility, architecture needs, risk, and cost at a glance.

## Theoretical Framework

Every AI use case is classified along four dimensions:

### 1. Epistemic Demand (Cognitive Complexity)
Determines the AI approach and engineering scaffolding required.
- **Transductive**: Format change, structure preservation (e.g., translation, JSON conversion)
- **Extractive/Summarization**: Reduce data to dense subset without losing core truth
- **Generative/Synthetic**: Create new artifacts (code, images, narratives)
- **Evaluative/Critical**: Assess quality, logic, or ethics of existing information

### 2. Data Grounding (Source Reliability)
Determines the system architecture.
- **Closed-World (Grounded)**: Answer exists in provided context → RAG pipeline
- **Open-World (Unbound)**: Answer from model weights → fine-tuned / prompt-engineered
- **Augmented (RAG+Tools)**: Hybrid with external tools/search → agent architecture

### 3. Operational Objective (Action Type — NIST)
The business entry point — what does the human need the system to *do*?
- **Facilitating Goals**: Content creation, synthesis, drafting
- **Perceptual Tasks**: Pattern recognition in sensory/data (OCR, anomaly detection)
- **Cognitive Tasks**: Multi-step reasoning, planning, forecasting
- **Physical/Functional**: Task execution in digital/physical environments (RPA, browser agents)

### 4. Degree of Determinism (Correctness Metric)
Determines the level of human oversight and confidence thresholds needed.
- **Deterministic (Objective)**: Single correct answer → automatable with high confidence
- **Probabilistic (Subjective)**: Many "good" answers → human-in-the-loop review

### Dimensional Complexity Matrix

| Dimension | Low Complexity | High Complexity |
|---|---|---|
| Epistemic Demand | Transduction (format change) | Strategic planning / evaluative reasoning |
| Data Grounding | Closed-world (RAG over known docs) | Open-world (pure generation from weights) |
| Determinism | Rule-based / objective correctness | Creative / subjective quality |
| Data Structure | Structured (tables, JSON, forms) | Unstructured (video, audio, natural language) |

### Improvement Vectors (Performance Debugging)
- **High Epistemic Demand** → Chain-of-Thought, multi-agent workflows, structured decomposition
- **Low Data Grounding** → RAG, tool use, retrieval augmentation to anchor outputs
- **High Determinism Required** → Symbolic AI (code execution, calculators) over language prediction
- **Unstructured Input** → Pre-processing pipelines, modality-specific models, OCR/transcription front-ends

## Current Work To-Dos
- [ ] Define business function taxonomy (sales, marketing, ops, support, finance, HR, product, legal)
- [ ] Map AI capabilities to each business function using the 4-dimension framework
- [ ] Inventory current tools/providers per capability
- [ ] Evaluate maturity levels, cost, and real-world feasibility
- [ ] Build catalogue entries with full dimensional tagging

## Current Hypotheses
1. **H1 — Multimodal AI is production-ready for more tasks than businesses assume**: Most businesses are only using text LLMs; vision, audio, and agentic workflows are underutilized. *Prediction: 60-70% of common business tasks have at least one production-ready AI solution.*
2. **H2 — Integration complexity, not model capability, is the bottleneck**: The main barrier is plumbing (APIs, pipelines, UIs), not what models can do. *Prediction: Deterministic + structured tasks are easy to integrate; probabilistic + unstructured tasks remain hard.*
3. **H3 — Commodity tooling exists for 80% of common use cases**: Open-source + API solutions cover most needs; custom training is rarely required. *Prediction: Closed-world + transductive tasks are fully commoditized; open-world + evaluative tasks still need bespoke solutions.*
4. **H4 — The Determinism dimension predicts deployment success**: Use cases with high determinism requirements but low current AI determinism are where most AI projects fail. *Prediction: This misalignment explains the majority of "AI didn't work for us" outcomes.*

## Phase 1: Foundations
- [x] Repository initialized
- [x] Plan and journal templates set up
- [x] Theoretical framework defined (4 dimensions)
- [ ] Define business function taxonomy
- [ ] Map AI modalities to the 4-dimension framework
- [ ] Update catalogue templates with dimensional tagging

## Phase 2: Tool Inventory
- [ ] Survey current multimodal AI tools and providers
- [ ] Catalogue per business function with capability matrix
- [ ] Tag each tool's sweet spot on the 4 dimensions
- [ ] Assess pricing models and cost structures

## Phase 3: Deep Dives
- [ ] Select 3-5 high-impact business functions for detailed case studies
- [ ] Document implementation patterns (RAG, agents, multi-modal pipelines)
- [ ] Identify gaps where dimension mismatch causes failures
- [ ] Map improvement vectors to real tooling options

## Done Work
- [x] Repository initialized
- [x] Plan and journal templates set up
- [x] Multi-dimensional classification framework adopted (NIST/HAI/Sarker 2022)
