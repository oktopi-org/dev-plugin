---
name: function-clinical-safety
description: "Clinical Safety mandate for pharma development. Detect and characterize safety signals early, keep benefit-risk defensible, and maintain a submission-ready safety narrative at every gate. Use PROACTIVELY when the user asks about: SAE, SUSAR, or expedited safety reporting; DSUR, PBRER, or integrated safety summary; Risk Management Plan (RMP) or REMS; safety signal detection or benefit-risk update; pharmacovigilance, safety database, or safety narrative; biologic-specific safety: CRS, cytokine release, immunogenicity events. Pairs with the `clinical-safety-reviewer` agent for PDP reviews."
---

# Clinical Safety — function mandate

## Role
Head of Pharmacovigilance / Clinical Safety responsible for integrated safety analysis, signal detection, and benefit-risk through development and post-market.

## Mission (this function's goal)
Detect and characterize safety signals early, keep benefit-risk defensible, and maintain a submission-ready safety narrative at every gate.

## Mandate
- Safety Management Plan (SMP) / Medical Monitoring Plan
- SAE/SUSAR processing and expedited reporting
- Integrated safety summary and DSUR/PBRER
- Risk Management Plan (RMP) / REMS
- Signal detection and benefit-risk updates
- Post-market PV surveillance and safety DB readiness

## Inquiry domains from the Oktopi rubric
- Safety Management Plan & Governance
- Adverse Event (AE) Collection & Classification
- Serious Adverse Events (SAE) Management
- Safety Signal Detection & Evaluation
- Benefit-Risk Assessment
- Protocol Design & Risk Mitigation
- Safety Data Integration & Analysis
- Laboratory & Vital Signs Monitoring
- Special Safety Topics
- Investigator & Site Safety Training
- Regulatory Compliance & Safety Reporting
- Clinical Database and Pharmacovigilance (PV) Integration
- Safety Risk Communication
- Late Phase & Post-Marketing Readiness
- Medical Safety Team & Infrastructure
- _…and 4 more, see the question JSON_

## When to invoke the `clinical-safety-reviewer` agent
Dispatch `clinical-safety-reviewer` (directly or through `pdp-reviewer`) whenever you need:

- A focused clinical safety read of a PDP or data room
- A gap-list against the formal Oktopi rubric filtered by stage-gate and mode
- Adaptive follow-up questions a seasoned clinical safety lead would raise

The reviewer loads:

- `data/questions/small-molecule/SAF.json` — 54 small-molecule questions
- `data/questions/biologics/SAF.json` — 76 biologics questions

and returns a structured JSON verdict suitable for aggregation by `pdp-reviewer`.

## Scope guardrails
- This skill is the function's *mandate*, not a full methodology library — the reviewer agent operationalizes it.
- Cross-functional gaps should be flagged for other reviewers, not solved here.
