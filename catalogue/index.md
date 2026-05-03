# Catalogue Index

A multi-dimensional map of AI capabilities for business use. Every entry is tagged on four axes from the [NIST/HAI/Sarker 2022 framework](../plan.md#theoretical-framework).

## Quick Reference: The Four Dimensions

1. **Epistemic Demand** — How complex is the thinking? (Transductive → Evaluative)
2. **Data Grounding** — Where does the truth come from? (Closed → Open → Augmented)
3. **Operational Objective** — What does the system *do*? (Facilitate → Perceive → Reason → Execute)
4. **Degree of Determinism** — How do we measure success? (Objective → Subjective)

## By Business Function

Each function page lists AI-applicable tasks with full dimensional profiles.

- [Sales & Business Development](business_functions/sales.md)
- [Marketing & Content](business_functions/marketing.md)
- [Customer Support](business_functions/support.md)
- [Operations & Logistics](business_functions/operations.md)
- [Finance & Accounting](business_functions/finance.md)
- [Human Resources](business_functions/hr.md)
- [Product & Engineering](business_functions/product.md)
- [Legal & Compliance](business_functions/legal.md)

## By AI Modality

Which input/output types current models handle well.

- **Text**: Generation, analysis, summarization, conversation ★★★★★
- **Vision**: OCR, document parsing, image understanding, UI analysis ★★★★☆
- **Image Generation**: Product mockups, marketing assets, design ★★★★☆
- **Audio/Speech**: Transcription, TTS, voice agents, audio analysis ★★★★☆
- **Video**: Generation, editing, summarization ★★★☆☆
- **Code**: Generation, review, debugging, migration ★★★★★
- **Agents**: Multi-step workflows, tool use, RAG orchestration ★★★☆☆

## By Determinism (Deployment Risk)

The most business-critical lens — how much can you trust the output?

**Fully Automatable** (Deterministic tasks with mature AI):
- Data format conversion, extraction from structured documents
- Translation of standard business documents
- Code generation from clear specs with test validation

**Human-in-the-Loop** (Probabilistic with high business value):
- Marketing copy, sales outreach drafts
- Customer support responses (AI drafts, human approves)
- Legal document review (AI flags, human decides)

**Experimental / High Risk** (High epistemic demand + low determinism):
- Strategic planning and forecasting
- Hiring recommendations
- Autonomous negotiation or financial trading

## Tools Directory

- [Text & LLMs](tools/llm_providers.md)
- [Vision & Document AI](tools/vision.md)
- [Audio & Speech](tools/audio.md)
- [Image & Video Generation](tools/image_video.md)
- [Agents & Orchestration](tools/agents.md)
