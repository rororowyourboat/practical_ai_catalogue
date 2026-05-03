# FCTAF Grounding Assessment

An honest assessment of where FCTAF is empirically grounded, where it's theoretically plausible but unvalidated, and where it's speculative.

---

## Well-Grounded (Strong Prior Art)

### 1. The Pipeline Model
**Status**: ✅ Well-supported

The idea that tasks can be decomposed into distinct processing stages is well-established:
- Parasuraman et al. (2000) proposed 4 information processing stages for human-automation systems
- Endsley (1995) proposed 3 levels of situation awareness (perception → comprehension → projection)
- Cognitive Task Analysis (Schraagen et al. 2000) provides methodological backing

**What's new in FCTAF**: Adding a 5th stage (Transduction) specific to AI output formatting, and the explicit mapping to failure modes at each stage. The specific 5-stage decomposition is novel but structurally similar to established models.

**Risk**: The 5 stages might not be the *right* 5 — could be too coarse (missing sub-stages) or too fine (some stages merge in practice). No empirical validation that these specific boundaries capture the right failure transitions.

### 2. Automation Levels → Node Types
**Status**: ✅ Well-supported

The Code/AI/Human node taxonomy is a simplified version of established automation taxonomies:
- Sheridan & Verplank (1978): 10 levels from full manual to full automation
- Parasuraman et al. (2000): Applied across 4 processing stages

**What's new in FCTAF**: Collapsing the 10-level scale into 3 discrete actor types with distinct failure *characters*. This is a useful simplification but loses granularity.

**Risk**: Real systems don't cleanly map to 3 node types. A "Human with AI assistance" node is common but not modeled. Mid-stage handoffs (Human delegates to AI within a stage) are flagged as an open question.

### 3. Synthesis Depth → Chain-of-Thought
**Status**: ✅ Strong empirical support

Wei et al. (2022) demonstrated that task complexity (reasoning steps) directly predicts LLM failure, and that explicit step decomposition (CoT) mitigates it. Bubeck et al. (2023) showed capability varies systematically with task difficulty.

**What's new in FCTAF**: Framing this as a continuous lever rather than binary (CoT vs. no-CoT), and connecting it to architecture selection (1-hop = API call, multi-hop = RAG + CoT, deep = multi-agent).

### 4. Hallucination as Stage IV Failure
**Status**: ✅ Well-documented

Multiple surveys (Huang 2023, Zhang 2023, Mündler 2023) characterize hallucination types and detection methods. RAGAS (Es 2023) operationalizes faithfulness measurement.

**What's new in FCTAF**: Positioning hallucination not as a monolithic "model problem" but as a Stage IV failure that can have upstream causes (Stage III provided wrong data via dynamic edge, Stage II selected wrong source).

---

## Plausible But Unvalidated (Theoretical)

### 5. Edge Taxonomy (Deterministic / Dynamic / Feedback)
**Status**: ⚠️ Plausible, no direct prior art

The idea of classifying inter-stage connections by their failure propagation risk is novel. Related concepts exist:
- Gao et al. (2023) describe RAG pipeline failures but don't formalize the connection types
- Zaharia et al. (2024) argue for compound systems but don't classify the connections
- Workflow graph theory classifies edges (dataflow, control flow) but not by propagation risk

**What's new in FCTAF**: The specific taxonomy of Deterministic (contract-enforced), Dynamic (open handoff), and Feedback (loop back) edges with propagation risk ratings. The claim that dynamic edges are the primary propagation vector (H6).

**Risk**: This is the most novel and least grounded part of FCTAF. We have no empirical evidence that:
- These 3 edge types capture the important variation
- Dynamic edges are actually the primary propagation vector
- Replacing dynamic edges with deterministic ones would eliminate most silent failures

**What would validate it**: Instrumented pipeline studies measuring failure rates across edge types in production AI systems. Currently no such benchmark exists.

### 6. Epistemic Friction as a Lever
**Status**: ⚠️ Grounded in theory, not in AI-specific data

Pirolli & Card (1999) provide strong theoretical grounding for information seeking cost-benefit tradeoffs. The extension to AI retrieval (messy sources cost more) is intuitive.

**What's new in FCTAF**: Framing source messiness as a continuous lever that predicts Stage III difficulty and pre-processing requirements.

**Risk**: The mapping from "structured → semi-structured → entropic" to "no pre-processing → light → heavy" is a rule of thumb, not a validated model. The actual cost multiplier (claimed H5: 10x) is speculative. Real friction depends on the specific model, the specific data, and the specific task.

### 7. Intent Variance as a Lever
**Status**: ⚠️ Partially grounded

The deterministic vs. probabilistic distinction is well-established in NLP evaluation. But framing it as a *continuous lever* that predicts deployment success (H4) is a hypothesis, not a finding.

**Risk**: Some divergent tasks (creative writing) can be automated successfully with the right user expectations. Some convergent tasks (arithmetic) can fail if the model doesn't have the right tooling. Variance is necessary but not sufficient for predicting deployment success.

---

## Speculative (Novel Claims)

### 8. H2: Stage I-II Failures Dominate
**Status**: 🔴 Speculative — plausible but no data

This is FCTAF's strongest practical claim and its weakest empirical position. We argue that most "AI didn't work" outcomes stem from poor intent framing (Stage I) or wrong source selection (Stage II), not from model capability limitations.

**Evidence for**: Anecdotal. RAG pipeline papers (Gao 2023) show that retrieval quality dominates end-to-end performance. "Lost in the Middle" (Liu 2023) shows that providing the right context matters more than model size.

**Evidence against**: No systematic study has measured failure distribution across pipeline stages in production systems. It's possible that Stage IV (hallucination) actually dominates and we're just better at detecting it.

**What would validate it**: A large-scale study of production AI system failures, categorized by FCTAF stage. Currently doesn't exist.

### 9. H6: Dynamic Edges Are the Primary Propagation Vector
**Status**: 🔴 Speculative

This follows from the edge taxonomy, which is itself unvalidated. It's a strong, testable claim.

**What would validate it**: Instrumented pipeline studies comparing failure rates in systems with deterministic vs. dynamic inter-stage connections.

### 10. H5: Epistemic Friction 10x Cost Driver
**Status**: 🔴 Speculative

The 10x claim is a hypothesis, not a measurement. Real costs depend on the specific combination of friction + depth + variance.

### 11. Upstream Failures Present as Downstream Symptoms
**Status**: ⚠️ Plausible, partially documented

Gao et al. (2023) document this pattern in RAG systems (retrieval failures look like generation failures). But the general claim — that this is the *dominant* failure pattern in AI systems — is unvalidated.

---

## Missing Prior Art

Areas where we should find more resources:

1. **Production AI failure studies**: Are there post-mortems or incident reports from production AI systems that categorize failures by pipeline stage?
2. **Workflow graph theory**: We reference it but haven't cited specific formalisms for edge classification in dataflow systems.
3. **Multi-agent handoff failures**: As agents become more common, what are the documented failure modes at handoff points?
4. **Human-AI team performance**: Studies measuring how different node assignments affect task outcomes.
5. **Confidence calibration in pipelines**: Kadavath (2022) studies single-model calibration. Are there studies of confidence propagation through multi-stage pipelines?
6. **Formal verification of AI pipelines**: Work on proving properties of compound AI systems (contract enforcement at deterministic edges).
