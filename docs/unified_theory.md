# Unified Theory of Epistemic Engineering

This document provides the formal synthesis of the three pillars supporting the Practical AI Catalogue: **FCTAF v2**, **IR Design Space**, and **Epistemic Architecture**.

## 1. The Engineering Thesis
AI implementation is not a software problem; it is an **Epistemic Engineering** problem. Failure occurs when there is a mismatch between the **Territory** (the business reality), the **Map** (the data representation), and the **View** (the AI's output).

## 2. The Unified Stack

### Layer 1: Epistemic Discipline (Theory)
*Ref: map_is_not_territory*
Governs the "Commitment Scale." It ensures we don't collapse the **Logical View** (what the system is) into the **Physical View** (which LLM we are using). It forces us to acknowledge that every view is **Structured Loss**.

### Layer 2: Technical Specification (Design)
*Ref: information_retreival*
Provides the inventory of **Design Patterns**. It tells us *how* to represent data (Graph vs. Vector) and *how* to retrieve it (Semantic vs. Lexical) based on the query landscape.

### Layer 3: Operational Diagnosis (Process)
*Ref: practical_ai_catalogue / FCTAF*
Provides the **Supply Chain**. It breaks the task into five discrete stages and assigns specific **Nodes** (AI, Code, or Human) and **Edges** (Contracts) to manage the flow of information.

---

## 3. Structural Alignment Matrix

| FCTAF Stage | View Type | Epistemic Objective | Primary Metric |
|---|---|---|---|
| **I. Intent Framing** | Operational | Define the target **View** | Legibility |
| **II. Epistemic Mapping** | Logical | Select the correct **Framework** | Identifiability |
| **III. Info Retrieval** | Physical | Extract from the **System** | Observability |
| **IV. Logical Synthesis** | Behavioral | Reason over the **Framework** | Faithfulness |
| **V. Transduction** | Functional | Project the final **View** | Determinism |

---

## 4. The Complexity Levers as System Properties

We characterize the "Difficulty Profile" of a task using these formal properties:

1.  **Synthesis Depth**: Corresponds to the **Behavioral View** complexity. High depth requires **Agentic Loops** and **Multi-hop Reasoning**.
2.  **Epistemic Friction**: Corresponds to the **Observability** of the raw System. High friction requires **Semantic Chunking** and **Context Optimization**.
3.  **Intent Variance**: Corresponds to **Divergence** in the Functional View. High variance requires **Human-in-the-loop (HITL) Nodes**.

---

## 5. Diagnostic Protocol
To troubleshoot an AI system:
1.  **Stage Location**: At which FCTAF stage is the symptom visible?
2.  **Node Assignment**: Is the Node Type (AI/Code/Human) appropriate for that stage's complexity?
3.  **Edge Contract**: Is the failure a **Propagation Error** caused by a Dynamic Edge?
4.  **Design Mismatch**: Does the IR Technique (e.g., Vector Search) match the Query Landscape (e.g., Procedural)?
5.  **Conceptual Collapse**: Are we confusing the "Tool" (Physical) with the "Task" (Functional)?
