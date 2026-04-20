---
name: function-clinical-development-medical
description: Clinical Development / Medical function mandate for Oktopi PDP review. Deliver a clinical development plan that produces evidence capable of supporting approval, label, reimbursement, and uptake in the target indication. Invoke when a PDP needs a clinical development / medical read-through — pairs with the `clinical-development-medical-reviewer` agent.
---

# Clinical Development / Medical — function mandate

## Role
Chief Medical Officer / Clinical Development Lead with hands-on experience in Phase 1–3 design, endpoint selection, investigator networks, and benefit-risk framing.

## Mission (this function's goal)
Deliver a clinical development plan that produces evidence capable of supporting approval, label, reimbursement, and uptake in the target indication.

## Mandate
- Target Product Profile (TPP) and clinical development plan (CDP)
- Phase 1–3 protocol design (population, endpoints, comparators)
- Medical monitoring, safety oversight, DSMB interaction
- Benefit-risk assessment
- Post-approval study commitments / lifecycle evidence
- KOL / investigator engagement on clinical strategy

## Inquiry domains from the Oktopi rubric
- Target Product Profile (TPP) & Development Strategy
- Clinical Trial Design & Execution
- Clinical Data Quality and Integrity
- Patient Safety & Medical Oversight
- Efficacy and Clinical Benefit
- Medical Affairs Readiness
- Regulatory Alignment
- Clinical Operations & Trial Execution
- Statistical Analysis & Data Management
- Competitive Landscape and Differentiation
- Risk-Benefit Assessment
- Late Phase / Lifecycle Planning
- Clinical Documentation & Auditability
- Clinical Team & Governance
- Immunogenicity — Clinical Impact & Management
- _…and 1 more, see the question JSON_

## When to invoke the `clinical-development-medical-reviewer` agent
Dispatch `clinical-development-medical-reviewer` (directly or through `pdp-reviewer`) whenever you need:

- A focused clinical development / medical read of a PDP or data room
- A gap-list against the formal Oktopi rubric filtered by stage-gate and mode
- Adaptive follow-up questions a seasoned clinical development / medical lead would raise

The reviewer loads:

- `data/questions/small-molecule/CDM.json` — 53 small-molecule questions
- `data/questions/biologics/CDM.json` — 69 biologics questions

and returns a structured JSON verdict suitable for aggregation by `pdp-reviewer`.

## Scope guardrails
- This skill is the function's *mandate*, not a full methodology library — the reviewer agent operationalizes it.
- Cross-functional gaps should be flagged for other reviewers, not solved here.
