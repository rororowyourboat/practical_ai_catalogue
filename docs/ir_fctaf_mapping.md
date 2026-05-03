# Mapping IR Design Space to FCTAF v2

This document maps the theoretical foundations in **Information Retrieval as Epistemic Architecture** to the operational stages of the **Functional Cognitive Task-Analytic Framework (FCTAF)**.

## The Resolution Matrix
Use this matrix to identify which Information Retrieval (IR) design patterns solve specific task failures in the AI supply chain.

| FCTAF Stage | Failure Mode | IR Design Space "Fix" | DS Module |
| :--- | :--- | :--- | :--- |
| **I. Intent Framing** | **Ambiguity Drift:** System solves the wrong problem. | **Query Landscape Mapping:** Classify if the need is Fact, Procedural, or Analytical. | [[07]] |
| **II. Epistemic Mapping** | **Tool-Use Blindness:** Wrong source or tool selected. | **Data vs Query Landscape:** Aligning the data representation to the query archetype. | [[05]], [[06]] |
| **III. Info Retrieval** | **Precision Fatigue:** Noise overwhelms the relevant signal. | **Hybrid Retrieval & Reranking:** Use Sparse+Dense retrieval followed by Cross-Encoders. | [[09]], [[10]] |
| **IV. Logical Synthesis** | **Hallucination:** "Stitching" errors across disparate data points. | **Dynamic Retrieval Loops:** Implement agentic feedback to verify synthesis against sources. | [[15]], [[22]] |
| **V. Transduction** | **Schema Violation:** Correct info in the wrong format. | **Post-retrieval Processing:** Use structured extraction and format-aware generation. | [[16]] |

---

## Lever-Specific IR Strategies

How the 3 Complexity Levers are managed through IR Design:

### 1. Synthesis Depth (The Reasoning Lever)
*   **Low Depth (1-hop):** Standard RAG pattern (Semantic Search).
*   **High Depth (5+ hops):** Requires **Graph Representation [[08]]** and **Multi-step Agentic Retrieval [[22]]**.

### 2. Epistemic Friction (The Data Lever)
*   **Low Friction (Structured):** **Lexical/SQL Retrieval [[09]]** with strict metadata facets.
*   **High Friction (Entropic):** **Semantic Chunking [[13]]** and **Context Optimization [[14]]** (e.g., lost-in-the-middle fixes).

### 3. Intent Variance (The Goal Lever)
*   **Convergent (Fixed goal):** Pre-computed indices and static prompt templates.
*   **Divergent (Exploratory):** **Interactive Retrieval Loops [[15]]** and **Exploratory/Faceted Querying [[07]]**.

---

## Edge Engineering with IR
The transition between FCTAF stages (Edges) is governed by the quality of the IR "View."

*   **Deterministic Edges:** Require **Post-retrieval Processing [[16]]** to ensure the "View" matches a hard schema before passing to a Code Node.
*   **Dynamic Edges:** Rely on **Context Optimization [[14]]** to ensure the most relevant information is prominent in the LLM's limited attention window.
*   **Feedback Edges:** Operationalize the **Dynamic Retrieval Loop [[15]]**, where failure at a downstream stage triggers a refined query upstream.
