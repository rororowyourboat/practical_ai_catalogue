# Catalogue Index

A diagnostic catalogue of AI capabilities for business use, built on the [FCTAF framework](../docs/fctaf.md). Every entry is profiled as a **5-stage pipeline** with **3 complexity levers**, enabling failure prediction, architecture selection, and per-stage measurement.

## Quick Reference

### The 5 Stages (Where tasks break)
1. **Intent Framing** — Did we understand the right problem?
2. **Epistemic Mapping** — Did we look in the right place?
3. **Info Retrieval** — Did we get the right data?
4. **Logical Synthesis** — Did we reason correctly?
5. **Transduction** — Did we deliver in the right shape?

### The 3 Levers (How hard is it)
- **Synthesis Depth** — Unimodal → Multi-hop → Deep Synthesis
- **Epistemic Friction** — Structured → Semi-structured → Entropic
- **Intent Variance** — Convergent → Guided → Divergent

### The Diagnostic Map (What to fix)
| Profile | Failure Point | Fix |
|---|---|---|
| Open-ended goal | Stage I | Iterative scoping |
| Messy documents | Stage III | Vector search / reranking |
| Complex logic | Stage IV | CoT / multi-agent |
| Strict output format | Stage V | Few-shot / structured output |
| Wrong data source | Stage II | Router agents |

---

## By Business Function

Each function page lists AI-applicable tasks with full FCTAF pipeline analysis and complexity profiles.

- [Sales & Business Development](business_functions/sales.md)
- [Marketing & Content](business_functions/marketing.md)
- [Customer Support](business_functions/support.md)
- [Operations & Logistics](business_functions/operations.md)
- [Finance & Accounting](business_functions/finance.md)
- [Human Resources](business_functions/hr.md)
- [Product & Engineering](business_functions/product.md)
- [Legal & Compliance](business_functions/legal.md)

## By AI Modality

- **Text**: Generation, analysis, summarization, conversation ★★★★★
- **Vision**: OCR, document parsing, image understanding ★★★★☆
- **Image Generation**: Product mockups, marketing assets ★★★★☆
- **Audio/Speech**: Transcription, TTS, voice agents ★★★★☆
- **Video**: Generation, editing, summarization ★★★☆☆
- **Code**: Generation, review, debugging, migration ★★★★★
- **Agents**: Multi-step workflows, tool use, RAG orchestration ★★★☆☆

## By Deployment Risk (Intent Variance)

**Fully Automatable** (Convergent — deterministic):
- Data format conversion, extraction from structured documents
- Translation of standard business documents
- Code generation from clear specs with test validation

**Human-in-the-Loop** (Guided — constrained creativity):
- Marketing copy, sales outreach drafts
- Customer support responses (AI drafts, human approves)
- Legal document review (AI flags, human decides)

**Experimental / High Risk** (Divergent — open-ended):
- Strategic planning and forecasting
- Hiring recommendations
- Autonomous negotiation or financial trading

## Tools Directory

Tools rated by their FCTAF stage affinity and complexity tolerance.

- [Text & LLMs](tools/llm_providers.md)
- [Vision & Document AI](tools/vision.md)
- [Audio & Speech](tools/audio.md)
- [Image & Video Generation](tools/image_video.md)
- [Agents & Orchestration](tools/agents.md)
