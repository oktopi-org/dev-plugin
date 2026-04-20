---
name: review-stage-gate
description: Run a multi-function PDP review against a specific Oktopi stage-gate and mode
argument-hint: <SG1..SG9> <SR|OE|DD|RS> [small-molecule|biologics] [path-to-document]
---

# Review a PDP against an Oktopi stage-gate

Arguments (positional):

1. `stage_gate` — one of `SG1 SG2 SG3 SG4 SG5 SG6 SG7 SG8 SG9`
2. `mode` — one of `SR` (Strategic Readiness), `OE` (Operational Execution), `DD` (Due Diligence), `RS` (Regulatory Submission)
3. `modality` *(optional, default `small-molecule`)* — `small-molecule` or `biologics`
4. `document` *(optional)* — path or URL to the PDP / briefing deck / data room

## Workflow

1. Load `data/stage-gates.json` and confirm the stage-gate goal for `${1}`.
2. Open the matching stage-gate skill at `skills/stage-gate-${1:lower}/SKILL.md` to get the critical-question index for mode `${2}`.
3. For every function that has Critical questions at (`${1}`, `${2}`):
   - Dispatch the function's `<function>-reviewer` agent (see `data/functions.json` for the slug).
   - Brief it with: the stage-gate code, the mode, the modality, and the document.
   - Ask it to return: (a) go/no-go, (b) top-3 gaps with owners, (c) questions it could not evaluate.
4. Aggregate all function reports into a single stage-gate readiness summary with:
   - Overall readiness (Ready / Conditional / Not Ready)
   - Function-level heatmap (Critical gaps count per function)
   - Top cross-functional risks
   - Next-step recommendations before the gate review

## Guardrails

- Never assume evidence that is not in the provided document. Surface unknowns.
- When dispatching multiple function reviewers, launch them in parallel (single message, multiple tool uses).
- If the document is not provided, produce a *checklist template* with the prioritized questions instead of a review.
