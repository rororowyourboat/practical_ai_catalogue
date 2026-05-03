# The Epistemic Layer: Conceptual, Functional, and Logical Views

The `map_is_not_territory` research identifies that most architectural failures stem from **Conceptual Collapse**: when we mistake our representation for the reality it describes. In the context of AI Catalogue, this means mistaking a "Tool Review" for the "Business Capability" it enables.

## The Three-Layer Architecture of Understanding
To avoid collapse, we distinguish between three layers of any AI task or tool:

| Layer | Research Ref | Description | Catalogue Application |
|---|---|---|---|
| **The System (Territory)** | `building_is_cheap` | The raw reality: messy PDFs, erratic user behavior, shifting market needs. | **Epistemic Friction** (FCTAF Lever) |
| **The Framework (Map)** | `building_is_cheap` | The ontology: our choice of what exists (e.g., "A 'User' is an email address"). | **Stage II: Epistemic Mapping** |
| **The View (Projection)** | `building_is_cheap` | The subset of the framework shown to answer a specific question. | **Stage V: Transduction** |

---

## Architectural Views Compared
When evaluating a tool or design, we must specify *which view* we are using. Confusing these views is a primary failure mode.

*   **Functional View (What happens):** Mapping the task supply chain (FCTAF Stages).
*   **Logical View (What exists):** The node taxonomy (AI vs. Code vs. Human).
*   **Physical View (What actual things):** The specific vendors, APIs, and models (The Tool Inventory).
*   **Operational View (Context):** How the tool fits into the business function (Sales, Ops, Legal).

---

## Technical Debt and "Building is Cheap"
The core thesis of **`building_is_cheap.md`** is that *knowing what to build* is the bottleneck, not the building itself.

1.  **AI as a Coordination Surface:** Tools are not just automation; they are where a team's understanding of a domain becomes concrete.
2.  **Structured Lossyness:** Every view is a "deliberate lie." A RAG system's chunking strategy is a choice of what to hide. If we don't choose what to lose, we lose everything to noise.
3.  **The -ility Trap:** Beware of grading tools on vague "-ilities" (like "Scalability") without defining the failure condition (Ref: `system-properties-glossary`).

## Diagnostic Cross-Reference
Use the `system-properties-glossary` to define success metrics for FCTAF stages:

- **Stage III (Retrieval) Success:** High **Observability** and **Identifiability**.
- **Stage IV (Synthesis) Success:** High **Faithfulness** and **Explainability**.
- **Edge Success:** High **Idempotence** and **Determinism** (for Code Nodes).
