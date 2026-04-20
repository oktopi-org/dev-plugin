---
name: function-clinical-pharmacology
description: "Clinical Pharmacology function mandate for Oktopi PDP review. Ensure every dose decision — starting, escalation, Phase 3, and label — is anchored in a defensible exposure-response story. Invoke when a PDP needs a clinical pharmacology read-through — pairs with the `clinical-pharmacology-reviewer` agent."
---

# Clinical Pharmacology — function mandate

## Role
Clinical Pharmacology Lead responsible for human PK/PD, dose-exposure-response, DDI, special populations, and dose-selection.

## Mission (this function's goal)
Ensure every dose decision — starting, escalation, Phase 3, and label — is anchored in a defensible exposure-response story.

## Mandate
- Human PK characterization (linearity, accumulation, variability)
- Exposure-response modeling (efficacy + safety)
- DDI strategy (in vitro + clinical)
- Special populations (renal, hepatic, pediatric, geriatric, pregnancy)
- Pop-PK / QSP modeling support
- Label dose recommendation and dose-finding design

## Inquiry domains from the Oktopi rubric
- Clinical Pharmacology Strategy
- Pharmacokinetics (PK)
- Pharmacodynamics (PD) & Exposure–Response (E-R)
- Bioavailability / Bioequivalence / Formulation Bridging
- Drug-Drug Interactions (DDIs)
- Intrinsic and Extrinsic Factors
- Special Populations
- Population PK and Modeling
- Physiologically-Based PK (PBPK) Modeling
- Pediatric Plans & Regulatory Readiness
- Integration with Clinical & Safety Data
- Regulatory & Labeling Considerations
- Documentation & Auditability
- SC Bioavailability & Formulation / Process Bridging
- Biologic-Specific Drug Interactions
- _…and 4 more, see the question JSON_

## When to invoke the `clinical-pharmacology-reviewer` agent
Dispatch `clinical-pharmacology-reviewer` (directly or through `pdp-reviewer`) whenever you need:

- A focused clinical pharmacology read of a PDP or data room
- A gap-list against the formal Oktopi rubric filtered by stage-gate and mode
- Adaptive follow-up questions a seasoned clinical pharmacology lead would raise

The reviewer loads:

- `data/questions/small-molecule/CP.json` — 47 small-molecule questions
- `data/questions/biologics/CP.json` — 59 biologics questions

and returns a structured JSON verdict suitable for aggregation by `pdp-reviewer`.

## Scope guardrails
- This skill is the function's *mandate*, not a full methodology library — the reviewer agent operationalizes it.
- Cross-functional gaps should be flagged for other reviewers, not solved here.
