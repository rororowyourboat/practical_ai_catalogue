# FCTAF Resource Bibliography

Organized by FCTAF component. All citations verified via OpenAlex, Semantic Scholar, or arXiv APIs.

---

## A. Pipeline Stages & Task Decomposition

These papers ground the idea that AI tasks can be decomposed into distinct processing stages with different failure characteristics.

### A1. Parasuraman, Sheridan & Wickens (2000)
**"A model for types and levels of human interaction with automation"**
- *IEEE Transactions on Systems, Man, and Cybernetics — Part A: Systems and Humans*, 30(3), 286–297
- DOI: [10.1109/3468.844354](https://doi.org/10.1109/3468.844354)
- **Relevance**: Foundational. Proposes 4 information processing stages (information acquisition → information analysis → action selection → action implementation) and 10 levels of automation. FCTAF's 5-stage pipeline is a direct extension of this model, adapted for AI-native workflows. The stage-to-node assignment (Code/AI/Human) maps to their levels of automation.
- **FCTAF Component**: Pipeline stages, Node Taxonomy

### A2. Sheridan & Verplank (1978)
**"Human and Computer Control of Undersea Teleoperators"**
- *MIT Man-Machine Systems Lab Technical Report*
- DOI: [10.21236/ada057655](https://doi.org/10.21236/ada057655)
- **Relevance**: Original 10-level automation scale. Established the idea that automation is not binary (manual vs. automatic) but a spectrum. FCTAF's node taxonomy (Code/AI/Human) operationalizes this spectrum as discrete actor types at each pipeline stage.
- **FCTAF Component**: Node Taxonomy, automation levels

### A3. Endsley (1995)
**"Toward a Theory of Situation Awareness in Dynamic Systems"**
- *Human Factors*, 37(1), 32–64
- DOI: [10.1518/001872095779049543](https://doi.org/10.1518/001872095779049543)
- **Relevance**: Defines three levels of situation awareness: perception (Level 1), comprehension (Level 2), and projection (Level 3). Maps directly to FCTAF's Intent Framing (understanding what's happening), Epistemic Mapping (comprehending which sources matter), and Logical Synthesis (projecting forward to conclusions).
- **FCTAF Component**: Stages I, II, IV

### A4. Schraagen, Chipman & Shalin (2000)
**"Cognitive Task Analysis"**
- *Lawrence Erlbaum Associates*, 531 pages
- **Relevance**: Comprehensive methodology for decomposing expert tasks into cognitive components. Provides the analytical backbone for FCTAF's approach of breaking business tasks into pipeline stages with distinct cognitive demands.
- **FCTAF Component**: Pipeline methodology, task decomposition

### A5. Fleishman & Quaintance (1984)
**"Taxonomies of Human Performance: The Description of Human Tasks"**
- *Academic Press*, 514 pages
- **Relevance**: Identifies 52 cognitive, psychomotor, and physical abilities underlying task performance. FCTAF's Synthesis Depth lever is grounded in Fleishman's deductive reasoning ability taxonomy — the idea that reasoning complexity can be measured as a discrete, quantifiable dimension.
- **FCTAF Component**: Synthesis Depth lever, task difficulty profiling

---

## B. Node Taxonomy (Actor Types)

### B1. Bommasani et al. (2021)
**"On the Opportunities and Risks of Foundation Models"**
- *Stanford HAI*, arXiv:2108.07258
- DOI: [10.48550/arxiv.2108.07258](https://doi.org/10.48550/arxiv.2108.07258)
- **Relevance**: Defines emergent and unpredictable capabilities in foundation models. The "risks" section documents failure modes unique to AI actors (silent failures, distributional shift, stereotyping) — directly supports FCTAF's characterization of AI Nodes as failing "silently or plausibly."
- **FCTAF Component**: AI Node failure character

### B2. Raisch & Krakowski (2021)
**"Artificial Intelligence and Management: The Automation–Augmentation Paradox"**
- *Academy of Management Review*, 46(1), 192–210
- DOI: [10.5465/amr.2018.0072](https://doi.org/10.5465/amr.2018.0072)
- **Relevance**: Argues that AI both automates (replaces human action) and augments (enhances human capability), and that these are not opposite ends of a spectrum but orthogonal dimensions. Supports FCTAF's node assignment as a design decision rather than a simple automation level.
- **FCTAF Component**: Node assignment as design decision

---

## C. Edge Taxonomy & Failure Propagation

### C1. Gao et al. (2023)
**"Retrieval-Augmented Generation for Large Language Models: A Survey"**
- arXiv:2312.10997
- DOI: [10.48550/arxiv.2312.10997](https://doi.org/10.48550/arxiv.2312.10997)
- **Relevance**: Identifies failure modes across the RAG pipeline: retrieval failures (wrong chunks returned), ranking failures (right chunks but wrong order), and generation failures (right context but wrong synthesis). Maps directly to FCTAF's Stage III failures, and the propagation from Stage III to Stage IV across a dynamic edge.
- **FCTAF Component**: Edge failures, Stage III→IV propagation

### C2. Liu et al. (2023)
**"Lost in the Middle: How Language Models Use Long Contexts"**
- *TACL 2024*; arXiv:2307.03172
- DOI: [10.1162/tacl_a_00638](https://doi.org/10.1162/tacl_a_00638)
- **Relevance**: Demonstrates that LLMs fail to use information in the middle of long contexts — relevant data is retrieved but then ignored during synthesis. This is a specific instance of a dynamic edge failure: Stage III produces correct output but Stage IV (AI Node) fails to use it. A deterministic edge with relevance markers could mitigate this.
- **FCTAF Component**: Dynamic edge failure, Stage III→IV propagation

### C3. Mündler et al. (2023)
**"Self-Contradictory Hallucinations of Large Language Models: Evaluation, Detection and Mitigation"**
- arXiv:2305.15852
- DOI: [10.48550/arxiv.2305.15852](https://doi.org/10.48550/arxiv.2305.15852)
- **Relevance**: Documents self-contradiction as a failure mode where an AI Node generates output that contradicts its own earlier output within the same session. This is a failure that crosses a dynamic edge within Stage IV — the model doesn't detect its own inconsistency. Supports the need for feedback edges (grounding verification).
- **FCTAF Component**: Feedback edges, AI Node silent failure

---

## D. Complexity Levers

### D1. Pirolli & Card (1999)
**"Information Foraging"**
- *Psychological Review*, 106(4), 643–675
- DOI: [10.1037/0033-295X.106.4.643](https://doi.org/10.1037/0033-295X.106.4.643)
- **Relevance**: Foundational. Models information seeking as cost-benefit optimization — foragers allocate effort based on expected information gain. Grounds FCTAF's Epistemic Friction lever: high-friction sources have lower information gain per unit effort, making retrieval more expensive. Also grounds Stage II (Epistemic Mapping) — the decision of *where* to look is an information foraging decision.
- **FCTAF Component**: Epistemic Friction lever, Stage II

### D2. Pirolli (2007)
**"Information Foraging Theory: Adaptive Interaction with Information"**
- *Oxford University Press*
- **Relevance**: Book-length extension with ACT-R computational models of foraging behavior. Provides formal framework for modeling the cost-benefit tradeoffs in FCTAF's Epistemic Mapping stage and Epistemic Friction lever.
- **FCTAF Component**: Epistemic Friction lever (formal model)

### D3. Wei et al. (2022)
**"Chain-of-Thought Prompting Elicits Reasoning in Large Language Models"**
- *NeurIPS 2022*
- arXiv:2201.11903
- **Relevance**: Demonstrates that decomposing complex reasoning into intermediate steps improves LLM performance. Directly supports FCTAF's Synthesis Depth lever: tasks with high synthesis depth benefit from explicit step decomposition (chain-of-thought), which is the optimization strategy for Stage IV.
- **FCTAF Component**: Synthesis Depth lever, Stage IV optimization

### D4. Bubeck et al. (2023)
**"Sparks of Artificial General Intelligence: Early experiments with GPT-4"**
- arXiv:2303.12712
- DOI: [10.48550/arxiv.2303.12712](https://doi.org/10.48550/arxiv.2303.12712)
- **Relevance**: Systematic evaluation of GPT-4 across cognitive tasks of varying difficulty. Provides empirical data on how model capability varies with task complexity — relevant for understanding how model size shifts the effective Synthesis Depth.
- **FCTAF Component**: Synthesis Depth, model capability effects

---

## E. Hallucination & Faithfulness (Stage IV Failures)

### E1. Huang et al. (2023/2024)
**"A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions"**
- *ACM Transactions on Information Systems*, 2024
- DOI: [10.1145/3703155](https://doi.org/10.1145/3703155)
- **Relevance**: Categorizes hallucination into intrinsic (contradicting source), extrinsic (fabricating beyond source), and factual (wrong facts). Maps to FCTAF's Stage IV failure modes: intrinsic hallucination = synthesis contradicts retrieval (feedback edge to III would catch), extrinsic = AI Node generates beyond its data (needs grounding verification).
- **FCTAF Component**: Stage IV failure modes, Faithfulness metric

### E2. Zhang et al. (2023)
**"Siren's Song in the AI Ocean: A Survey on Hallucination in Large Language Models"**
- arXiv:2309.01219
- DOI: [10.48550/arxiv.2309.01219](https://doi.org/10.48550/arxiv.2309.01219)
- **Relevance**: Complementary hallucination survey with emphasis on detection and mitigation. Useful for FCTAF's diagnostic procedure — how to detect a Stage IV failure when it occurs at an AI Node.
- **FCTAF Component**: Stage IV diagnostics, Faithfulness metric

---

## F. Agent Architectures & Feedback Loops

### F1. Wang et al. (2023/2024)
**"A Survey on Large Language Model based Autonomous Agents"**
- *Frontiers of Computer Science*, 2024; arXiv:2308.11432
- DOI: [10.1007/s11704-024-40231-1](https://doi.org/10.1007/s11704-024-40231-1)
- **Relevance**: Systematic review of LLM agent architectures identifying four components: profiling, memory, planning, and action. Identifies failure modes in planning (maps to Stage IV), memory (maps to Stage III), and tool use (maps to Stage II). Directly relevant to FCTAF's pipeline + node + edge model for agent systems.
- **FCTAF Component**: Full pipeline, Node/Edge design for agents

### F2. Shinn et al. (2023)
**"Reflexion: Language Agents with Verbal Reinforcement Learning"**
- *NeurIPS 2023*; arXiv:2303.11366
- DOI: [10.48550/arxiv.2303.11366](https://doi.org/10.48550/arxiv.2303.11366)
- **Relevance**: Implements a feedback loop where an agent reflects on its own output and revises. This is a concrete instance of FCTAF's feedback edge pattern: Stage IV outputs are evaluated, failures are identified, and a delta signal is passed back for re-entry. Demonstrates that feedback edges with verbal reflection as the delta signal improve agent performance.
- **FCTAF Component**: Feedback edges, delta signal design

### F3. Yao et al. (2023)
**"ReAct: Synergizing Reasoning and Acting in Language Models"**
- *ICLR 2023*; arXiv:2210.03629
- **Relevance**: Integrates reasoning (Stage IV) with action/observation (Stages II-III) in an interleaved loop. This is a concrete implementation of FCTAF's feedback edge: the agent reasons, acts (retrieves from environment), observes, and reasons again. Models the interplay between Epistemic Mapping, Info Retrieval, and Logical Synthesis.
- **FCTAF Component**: Feedback edges, Stage II-III-IV loop

### F4. Mialon et al. (2023)
**"Augmented Language Models: a Survey"**
- *TMLR*; arXiv:2302.07842
- DOI: [10.48550/arxiv.2302.07842](https://doi.org/10.48550/arxiv.2302.07842)
- **Relevance**: Surveys three augmentation types: reasoning (Stage IV), tools (Stage II-III), and retrieval (Stage III). Directly maps to FCTAF's pipeline stages and provides architecture patterns for each.
- **FCTAF Component**: Stage II-III-IV augmentation patterns

---

## G. Evaluation Frameworks

### G1. Es et al. (2023/2024)
**"RAGAS: Automated Evaluation of Retrieval Augmented Generation"**
- *EACL 2024 Demo Track*
- DOI: [10.18653/v1/2024.eacl-demo.16](https://doi.org/10.18653/v1/2024.eacl-demo.16)
- **Relevance**: Introduces metrics for faithfulness, answer relevance, context precision, and context recall. Directly operationalizes evaluation of FCTAF's Stage III (context precision/recall) and Stage IV (faithfulness, answer relevance). The closest existing tool to FCTAF's per-stage evaluative metrics.
- **FCTAF Component**: Stage III-IV evaluative metrics

### G2. Liu et al. (2023)
**"G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment"**
- *EMNLP 2023*
- DOI: [10.18653/v1/2023.emnlp-main.153](https://doi.org/10.18653/v1/2023.emnlp-main.153)
- **Relevance**: Framework for using LLMs to evaluate NLG output quality with chain-of-thought scoring. Applicable to FCTAF's Stage V (Transduction) evaluation — assessing whether output format, tone, and content meet specifications.
- **FCTAF Component**: Stage V evaluative metrics

---

## H. AI Risk & Governance

### H1. NIST AI Risk Management Framework (2023)
**"AI Risk Management Framework (AI RMF 1.0)"**
- *NIST AI 100-1*, January 2023
- URL: [https://www.nist.gov/artificial-intelligence/ai-risk-management-framework](https://www.nist.gov/artificial-intelligence/ai-risk-management-framework)
- **Relevance**: Defines Trustworthy AI characteristics (validity, reliability, safety, security, resilience, accountability, transparency, explainability, privacy, fairness) and four governance functions (govern, map, measure, manage). The "map" function aligns with FCTAF's task profiling; "measure" aligns with per-stage evaluative metrics.
- **FCTAF Component**: Risk assessment, governance integration

---

## I. Compound Systems & Architecture

### I1. Zaharia et al. (2024)
**"The Shift from Models to Compound AI Systems"**
- *Berkeley AI Research Blog*, February 2024
- URL: [https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/](https://bair.berkeley.edu/blog/2024/02/18/compound-ai-systems/)
- **Relevance**: Argues that the frontier of AI is no longer individual models but compound systems — pipelines combining multiple models, verifiers, and tools. Directly justifies FCTAF's pipeline + edge approach. The key insight: "the outputs of compound systems depend on the interaction of multiple components" — this is exactly the edge taxonomy's concern.
- **FCTAF Component**: Edge taxonomy, compound system architecture

### I2. Sarker (2022)
**"AI-Based Modeling: Techniques, Applications and Research Issues Towards Automation, Intelligent and Smart Systems"**
- *SN Computer Science*, 3, 337
- DOI: [10.1007/s42979-022-01043-x](https://doi.org/10.1007/s42979-022-01043-x)
- **Relevance**: Reviews AI modeling techniques with a taxonomy of automation levels and intelligent system categories. Provides background context for FCTAF's classification of tasks by automation potential and cognitive demand.
- **FCTAF Component**: Task classification background

---

## J. Confidence & Calibration

### J1. Kadavath et al. (2022)
**"Language Models (Mostly) Know What They Know"**
- arXiv:2208.00604
- **Relevance**: Shows that LLMs can be calibrated to estimate their own uncertainty. Directly relevant to FCTAF's open question on confidence propagation — if each stage output carries a confidence score, downstream stages can decide whether to accept or trigger a feedback loop.
- **FCTAF Component**: Confidence propagation (v3 open question)

### J2. Li et al. (2023)
**"Benchmarking and Improving Generator-Validator Consistency of Language Models"**
- arXiv:2310.01846
- DOI: [10.48550/arXiv.2310.01846](https://doi.org/10.48550/arXiv.2310.01846)
- **Relevance**: Studies the gap between what LLMs generate and what they can validate. Maps to FCTAF's distinction between AI Node generation (Stage IV) and validation (feedback edge) — if a model can't validate its own output, the feedback loop is unreliable.
- **FCTAF Component**: Feedback edge reliability, confidence propagation

---

## Coverage Map

Which FCTAF components each resource grounds:

| Component | Primary Resources | Secondary Resources |
|---|---|---|
| **5-Stage Pipeline** | A1 (Parasuraman), A3 (Endsley), A4 (Schraagen) | F1 (Wang agents), F4 (Mialon ALM) |
| **Node Taxonomy** | A1 (Parasuraman), A2 (Sheridan), B1 (Bommasani) | B2 (Raisch automation-augmentation) |
| **Edge Taxonomy** | C1 (Gao RAG survey), C2 (Liu Lost in Middle) | I1 (Zaharia compound systems) |
| **Synthesis Depth** | A5 (Fleishman), D3 (Wei CoT) | D4 (Bubeck sparks) |
| **Epistemic Friction** | D1 (Pirolli IFT), D2 (Pirolli book) | C1 (Gao RAG survey) |
| **Intent Variance** | A1 (Parasuraman levels) | B2 (Raisch) |
| **Hallucination / Stage IV** | E1 (Huang survey), E2 (Zhang survey) | C3 (Mündler self-contradiction) |
| **Feedback Loops** | F2 (Reflexion), F3 (ReAct) | J2 (Li generator-validator) |
| **Evaluative Metrics** | G1 (RAGAS), G2 (G-Eval) | E1 (Huang hallucination metrics) |
| **Risk / Governance** | H1 (NIST AI RMF) | B1 (Bommasani foundation risks) |
| **Confidence Propagation** | J1 (Kadavath calibration) | J2 (Li consistency) |
