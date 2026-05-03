# FCTAF Example: Legal AI Question-Answering and Report Synthesis Bot

This example applies the **Functional Cognitive Task-Analytic Framework (FCTAF v2)** to a legal AI bot that answers questions and synthesizes reports over a legal dataset.

## Example System

**Task:**

> Given our company’s contracts, policies, prior memos, and relevant regulations, answer legal questions and generate a short risk report with citations.

**Example user question:**

> Can we terminate the Acme vendor agreement without penalty?

FCTAF treats this not as “one AI bot,” but as a **five-stage information supply chain**. The bot must clarify the question, choose sources, retrieve evidence, reason across that evidence, and produce a legally useful output.

---

## FCTAF Overview for This Use Case

| Stage | Diagnostic Question | Legal Bot Example | Main Failure Mode |
|---|---|---|---|
| I. Intent Framing | What exactly is being asked? | Determine which contract, jurisdiction, termination basis, and output type the user means. | Ambiguous legal question |
| II. Epistemic Mapping | Where should the bot look? | Select contract repository, amendments, SOWs, legal playbook, regulations, or prior memos. | Looks in wrong source |
| III. Info Retrieval | Did it retrieve the right evidence? | Extract termination clause, notice period, fee provision, amendment history, and SOW obligations. | Misses key clause/document |
| IV. Logical Synthesis | Did it reason correctly? | Combine contract terms, amendments, facts, and policy into a cautious conclusion. | Overconfident or unsupported legal conclusion |
| V. Transduction | Did it deliver in the right shape? | Produce memo/report with citations, caveats, risk rating, and next steps. | Wrong format, missing citations, missing caveats |

The important point: **the legal bot does not “just answer.”** It moves through a chain of decisions, and a failure at any stage can produce a bad legal answer.

---

## Stage I — Intent Framing

The raw question is under-specified:

> Can we terminate the Acme vendor agreement without penalty?

The system needs to clarify:

- Which Acme agreement?
- Which version is currently effective?
- Which jurisdiction governs?
- Is the user asking about termination for convenience, breach, insolvency, non-performance, or something else?
- What does “penalty” mean: early termination fee, damages, notice obligations, repayment of discounts, or minimum spend?
- Is the desired output legal advice, internal risk triage, or drafting support?

A good Stage I output might be:

```json
{
  "task_type": "contract_termination_analysis",
  "target_party": "Acme Corp",
  "contract_name": "Master Services Agreement",
  "question": "Can company terminate without early termination fee?",
  "jurisdiction": "New York",
  "assumed_termination_basis": "for convenience",
  "required_output": "risk memo with citations",
  "uncertainties": [
    "Need current executed agreement",
    "Need amendments",
    "Need factual reason for termination"
  ]
}
```

### Stage I Failure

If Stage I fails, the bot may answer the wrong legal question.

For example, the user may have meant:

> Can we terminate because Acme breached the SLA?

But the bot answers:

> Termination for convenience requires 60 days’ notice and a fee.

That may be a valid answer to a different question, but it is not the right answer here. The root cause is not retrieval or reasoning. It is an **intent framing failure**.

---

## Stage II — Epistemic Mapping

After clarifying the question, the bot decides where to look.

Possible legal sources include:

- Contract repository
- Amendments and statements of work
- Internal contract metadata
- Relevant jurisdictional law
- Prior legal memos
- Company legal playbook or risk policy
- Email negotiations, if permitted
- Litigation or regulatory databases, if relevant

A good Stage II output might be:

```json
{
  "source_plan": [
    {
      "source": "contract_repository",
      "reason": "primary agreement and amendments"
    },
    {
      "source": "clause_index",
      "reason": "termination, notice, fees, survival clauses"
    },
    {
      "source": "legal_playbook",
      "reason": "company risk thresholds"
    },
    {
      "source": "jurisdictional_law_database",
      "reason": "governing law and enforceability"
    }
  ],
  "excluded_sources": [
    {
      "source": "general_web_search",
      "reason": "not authoritative enough for legal analysis"
    }
  ]
}
```

### Stage II Failure

If the bot searches only the main contract but ignores amendments, it may miss an amendment changing the termination terms.

The final answer may look like a bad legal conclusion, but the primary failure happened earlier:

> The bot looked in the wrong place.

---

## Stage III — Info Retrieval

Now the bot extracts the relevant evidence.

For this question, relevant evidence might include:

- Section 12.2: termination for convenience
- Section 12.4: early termination fee
- Section 15: notice requirements
- Amendment 2: waived termination fee after year two
- SOW #4: separate minimum commitment
- Governing law clause
- Internal playbook rule: “High-risk if termination exposure exceeds $250k”

A good Stage III output might be:

```json
{
  "retrieved_evidence": [
    {
      "document": "Acme MSA",
      "section": "12.2",
      "text": "Customer may terminate for convenience upon 60 days written notice..."
    },
    {
      "document": "Amendment 2",
      "section": "3",
      "text": "Early termination fee shall not apply after the second anniversary..."
    },
    {
      "document": "SOW #4",
      "section": "5",
      "text": "Customer commits to minimum spend of $500,000 through Dec 31..."
    }
  ],
  "missing_evidence": [
    "Current contract anniversary date",
    "Spend already incurred under SOW #4"
  ]
}
```

### Stage III Failure

The bot may retrieve the termination clause but miss the SOW minimum commitment.

It might then say:

> No early termination fee applies.

That may be incomplete because the company may still owe money under the SOW. This is not necessarily hallucination. It is **retrieval incompleteness**.

---

## Stage IV — Logical Synthesis

Now the bot reasons across the evidence.

It needs to combine:

- Termination right
- Notice period
- Fee waiver
- Minimum spend obligation
- Timing
- Jurisdiction
- Company risk policy

A good synthesis might be:

> The company likely can terminate the MSA for convenience with 60 days’ notice and without the MSA early termination fee if the second anniversary has passed. However, SOW #4 may create separate payment exposure because of its minimum spend commitment. Therefore, the answer is not “without penalty” overall; it is “without MSA termination fee, but with potential SOW liability.”

A structured Stage IV output might be:

```json
{
  "conclusion": "Partial yes",
  "reasoning": [
    "MSA permits termination for convenience with 60 days notice.",
    "Amendment 2 waives early termination fee after second anniversary.",
    "SOW #4 creates independent minimum spend obligation.",
    "Therefore, termination may avoid the MSA fee but not necessarily all payment exposure."
  ],
  "risk_level": "medium",
  "confidence": "moderate",
  "open_issues": [
    "Confirm contract anniversary date",
    "Calculate remaining SOW minimum spend",
    "Confirm whether SOW survives termination of the MSA"
  ]
}
```

### Stage IV Failure

A synthesis failure would be an answer like:

> You can terminate without penalty.

That is too strong. It collapses several different legal concepts:

- Termination right
- Early termination fee
- Minimum spend obligation
- Damages exposure
- Procedural notice requirement

This is the classic legal AI danger: the answer sounds polished but is overconfident or under-nuanced.

---

## Stage V — Transduction

Finally, the bot formats the answer for the target user.

A useful legal report might look like:

```markdown
# Termination Analysis: Acme MSA

## Short Answer
The company likely may terminate the Acme MSA for convenience with 60 days’ written notice. However, termination may not be entirely “without penalty” because SOW #4 includes a separate minimum spend commitment.

## Key Support
- MSA §12.2 permits termination for convenience with 60 days’ notice.
- Amendment 2 §3 waives the early termination fee after the second anniversary.
- SOW #4 §5 includes a $500,000 minimum spend commitment through Dec 31.

## Risk Rating
Medium.

## Open Questions
1. Has the second anniversary passed?
2. How much spend remains under SOW #4?
3. Does SOW #4 survive termination of the MSA?

## Recommended Next Step
Legal should confirm the amendment history and calculate remaining SOW exposure before sending notice.
```

### Stage V Failure

The legal reasoning may be correct, but the output can still fail if it has:

- No citations
- Wrong memo format
- Missing caveats
- Too much legalese for a business user
- Not enough precision for counsel
- No risk rating
- No recommended next step

That is a **transduction failure**, not a reasoning failure.

---

## Node Assignment: Who Should Own Each Stage?

For legal AI, not every stage should be owned by a free-form AI model.

| Stage | Recommended Node | Why |
|---|---|---|
| I. Intent Framing | AI + human confirmation | Legal questions are often ambiguous. |
| II. Epistemic Mapping | Code + AI | Code routes to approved sources; AI helps classify source needs. |
| III. Info Retrieval | Code + AI | Search, vector retrieval, OCR, and extraction can be combined. |
| IV. Logical Synthesis | AI with human review | Legal reasoning is high-risk and often uncertain. |
| V. Transduction | Code + AI | Templates and schema enforcement reduce formatting/citation failures. |

A safer architecture is not:

```text
User → LLM → Answer
```

It is closer to:

```text
User
  → intent clarifier
  → source router
  → retrieval system
  → reasoning model
  → citation verifier
  → report template
  → human review if high risk
```

---

## Edge Design: How Failures Propagate

One of FCTAF’s main claims is that failures often propagate through weak handoffs between stages.

### Risky Architecture: Mostly Dynamic Edges

```text
User asks question
  ↓
LLM decides what to search
  ↓
LLM retrieves/summarizes documents
  ↓
LLM writes legal answer
```

This is risky because each handoff is fuzzy. If the intent is wrong, every later stage inherits the mistake.

### Safer Architecture: Deterministic Contracts Between Stages

```text
Intent Framing
  ↓ requires structured task JSON
Epistemic Mapping
  ↓ requires approved source list
Info Retrieval
  ↓ requires cited evidence objects
Logical Synthesis
  ↓ requires conclusion tied to evidence IDs
Transduction
  ↓ requires memo schema + citation check
```

For example, Stage III should not pass only a vague natural-language summary. It should pass evidence objects:

```json
{
  "evidence_id": "E3",
  "document": "SOW #4",
  "section": "5",
  "claim_supported": "Minimum spend commitment exists",
  "quoted_text": "Customer commits to minimum spend of $500,000..."
}
```

Then Stage IV must cite evidence IDs when making claims.

---

## Complexity Profile

| Lever | Rating | Why |
|---|---|---|
| Synthesis Depth | High | Requires combining contract terms, amendments, factual assumptions, legal policy, and risk thresholds. |
| Epistemic Friction | Medium–High | Contracts are semi-structured; scanned PDFs, amendments, side letters, and SOWs increase messiness. |
| Intent Variance | Medium–High | Legal questions are often ambiguous and may have multiple condition-dependent answers. |

This means the deployment risk is significant. This is not a simple chatbot. It is a **legal research and synthesis pipeline**.

---

## Likely Failure Points Predicted by FCTAF

1. **Stage I: Ambiguous question**
   - User asks “Can we terminate?” without specifying basis, contract version, or meaning of “penalty.”

2. **Stage II: Wrong source universe**
   - Bot ignores amendments, SOWs, company policies, or governing law.

3. **Stage III: Incomplete retrieval**
   - Bot retrieves the MSA but misses side letters, attachments, amendments, or minimum commitments.

4. **Stage IV: Overconfident synthesis**
   - Bot says “yes” when the real answer is “yes, but only under certain conditions.”

5. **Stage V: Poor legal output**
   - Missing citations, caveats, risk rating, attorney-review warning, or recommended next steps.

The most dangerous failure is probably not simply “the model makes something up.” It is:

> The bot retrieves incomplete but plausible evidence, then gives a confident legal answer.

---

## What FCTAF Tells Us to Build

For this legal AI bot, FCTAF suggests the system needs:

- Intent clarification before retrieval
- Approved legal source routing
- Document/version control
- Citation-grounded retrieval
- Evidence object schema
- Claim-to-citation checking
- Confidence and open-issue reporting
- Human review for high-risk outputs
- Strict report templates
- Audit logs

The architecture becomes less like a generic chat interface and more like a controlled legal analysis system.

---

## Short Version

For a legal QA/report bot:

```text
I. Intent Framing
Clarify legal question and assumptions.

II. Epistemic Mapping
Choose the correct legal/document sources.

III. Info Retrieval
Extract relevant clauses, cases, policies, and facts.

IV. Logical Synthesis
Reason across them into a cautious legal conclusion.

V. Transduction
Produce a memo/report with citations, caveats, and next steps.
```

The framework’s main value is that it separates different kinds of failure.

If the bot gives a bad answer, FCTAF helps ask:

> Was the question ambiguous, were the wrong sources selected, was the evidence incomplete, was the reasoning bad, or was the report badly formatted?

That is the core diagnostic power.
