# FCTAF Visualization Ideas

FCTAF has multiple dimensions: stages, nodes, edges, complexity levers, failures, and diagnostics. A single diagram can become overloaded, so the framework should use several complementary visuals depending on the context.

## 1. Core Pipeline Diagram

Use this as the default visual for explaining the five-stage FCTAF supply chain.

```text
┌────────────────┐   ┌──────────────────┐   ┌────────────────┐   ┌──────────────────┐   ┌───────────────┐
│ I. Intent      │ → │ II. Epistemic    │ → │ III. Info      │ → │ IV. Logical      │ → │ V. Trans-     │
│ Framing        │   │ Mapping          │   │ Retrieval      │   │ Synthesis        │   │ duction       │
└────────────────┘   └──────────────────┘   └────────────────┘   └──────────────────┘   └───────────────┘
 Ambiguity Drift      Tool-Use Blindness      Precision Fatigue     Hallucination         Schema Violation
```

This is best for introducing the framework at a high level.

---

## 2. Pipeline With Nodes and Edges

This is the most useful applied visual for a concrete use case.

```text
        AI + Human             Code + AI              Code + AI              AI + Human              Code + AI
            │                      │                      │                      │                      │
┌────────────────┐   ┌──────────────────┐   ┌────────────────┐   ┌──────────────────┐   ┌───────────────┐
│ Intent         │──▶│ Epistemic        │──▶│ Info           │──▶│ Logical          │──▶│ Transduction  │
│ Framing        │   │ Mapping          │   │ Retrieval      │   │ Synthesis        │   │               │
└────────────────┘   └──────────────────┘   └────────────────┘   └──────────────────┘   └───────────────┘
      │                       │                    │                       │                      │
   Clarified              Source plan        Evidence objects        Legal conclusion        Memo/report
   task JSON              approved list       with citations          + risk level            schema

       Deterministic edge      Deterministic edge      Dynamic/Feedback edge      Deterministic edge
```

This visual shows:

- who owns each stage: Code, AI, Human, or a combination
- what each stage emits
- whether each handoff is deterministic, dynamic, or feedback-based
- where failures can propagate silently

---

## 3. Swimlane Diagram by Actor

Use swimlanes to show node assignment and handoffs across Human, AI, and Code actors.

```text
Human      ── Clarify question ───────────────────────────── Review high-risk conclusion ── Approve memo
              ▲                                                                  │
AI         ── Draft intent JSON ── Classify source needs ── Extract evidence ── Synthesize answer ── Draft report
                                   │                    │                       │
Code       ───────────────────── Validate sources ─── Retrieve docs ─────── Check citations ───── Enforce schema
```

This helps explain that FCTAF is not “AI does everything.” It is a node-assignment model for deciding which actor should own each stage.

---

## 4. Failure Heatmap

A failure heatmap is useful for catalogue entries and stakeholder summaries.

| Stage | Failure Risk | Why |
|---|---:|---|
| I. Intent Framing | 🔴 High | Legal questions are ambiguous. |
| II. Epistemic Mapping | 🔴 High | Must choose correct documents, amendments, law, and policies. |
| III. Info Retrieval | 🟠 Medium–High | May miss clauses, side letters, or outdated versions. |
| IV. Logical Synthesis | 🔴 High | Legal reasoning is nuanced and conditional. |
| V. Transduction | 🟡 Medium | Templates and citation checks can control risk. |

This gives a quick answer to: **where will this system probably break?**

---

## 5. Complexity Lever Bar Chart

Use a compact bar chart to visualize the three FCTAF complexity levers.

```text
Legal QA / Report Bot

Synthesis Depth     █████████░  High
Epistemic Friction  ████████░░  Medium–High
Intent Variance     ████████░░  Medium–High
```

This is useful for comparing task difficulty across catalogue entries.

Example comparison:

| Task | Synthesis Depth | Epistemic Friction | Intent Variance |
|---|---:|---:|---:|
| Invoice extraction | Low | Medium | Low |
| Legal termination analysis | High | High | High |
| Customer support FAQ | Medium | Medium | Medium |
| Marketing copy draft | Medium | Low | High |

---

## 6. Failure Trace Diagram

This is one of the most important diagnostic visuals because FCTAF’s core claim is:

> Upstream failures present as downstream symptoms.

Example:

```text
Primary failure:
Stage II selected only main MSA
        │
        ▼
Stage III missed Amendment 2 and SOW #4
        │
        ▼
Stage IV produced incomplete conclusion
        │
        ▼
Observed symptom:
Final memo says “terminate without penalty”
```

This makes clear that the fix is not always “use a better model.” Sometimes the fix is source mapping, retrieval validation, or stronger edge contracts.

---

## 7. Architecture Pattern Diagram

Use this visual for builders and implementation planning.

```text
User Query
   │
   ▼
Intent Clarifier
   │ structured task JSON
   ▼
Source Router
   │ approved source list
   ▼
Retriever / OCR / Clause Extractor
   │ evidence objects
   ▼
Reasoning Model
   │ conclusion + cited claims
   ▼
Citation Verifier
   │ verified answer
   ▼
Report Generator
   │ schema-conformant memo
   ▼
Human Review Gate
```

This bridges the conceptual framework to a deployable system architecture.

---

## 8. Catalogue Card Layout

For catalogue entries, use a compact card format.

```text
Use Case: Legal Contract Termination Analysis

Pipeline:
Intent → Sources → Evidence → Reasoning → Memo

Node Profile:
I: AI+Human | II: Code+AI | III: Code+AI | IV: AI+Human | V: Code+AI

Edge Risk:
I→II: Low | II→III: Low | III→IV: High | IV→V: Low

Complexity:
Synthesis Depth:     High
Epistemic Friction:  Medium–High
Intent Variance:     Medium–High

Primary Predicted Failures:
1. Ambiguous question
2. Wrong source universe
3. Incomplete retrieval
4. Overconfident conclusion
```

This makes the catalogue more readable and gives each use case a consistent visual profile.

---

## Recommended Standard Visual Set

Use four standard visuals across the project:

1. **FCTAF Pipeline Diagram** — for explaining the framework.
2. **Applied Node/Edge Pipeline** — for each concrete use case.
3. **Complexity Profile Bar Chart** — for comparing difficulty.
4. **Failure Trace Diagram** — for diagnosing what went wrong.

For the legal AI example, the recommended applied visual is:

```text
Legal Question
   │
   ▼
[I] Intent Framing
AI + Human
Output: clarified legal task JSON
Failure: ambiguous question
   │ deterministic edge
   ▼
[II] Epistemic Mapping
Code + AI
Output: approved source plan
Failure: wrong source universe
   │ deterministic edge
   ▼
[III] Info Retrieval
Code + AI
Output: cited evidence objects
Failure: missed clause/amendment
   │ dynamic or feedback edge
   ▼
[IV] Logical Synthesis
AI + Human
Output: legal conclusion + risk rating
Failure: overconfident synthesis
   │ deterministic edge
   ▼
[V] Transduction
Code + AI
Output: memo with citations/caveats
Failure: bad report format
```

## Implementation Note

These visuals can start as Markdown text diagrams and later be converted to Mermaid diagrams for better rendering in GitHub or documentation sites.
