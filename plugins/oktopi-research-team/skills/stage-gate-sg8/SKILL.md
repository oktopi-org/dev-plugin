---
name: stage-gate-sg8
description: "Goal and readiness criteria for Oktopi stage-gate SG8: Regulatory Submission / Payer Engagement / Pre-Launch. Trigger when assessing PDP readiness to exit SG8."
---

# Stage Gate SG8: Regulatory Submission / Payer Engagement / Pre-Launch

**Goal.** Submit a reviewable NDA/BLA, finalize payer value dossier, and prepare commercial launch readiness.

**Primary focus areas.** NDA/BLA submission, labeling strategy, payer value dossier, launch readiness

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG8` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG8` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG8` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 75 | 100 | 84 | 117 |
| `PT` | 20 | 29 | 25 | 39 |
| `TM` | 41 | 74 | 41 | 57 |
| `CP` | 74 | 60 | 88 | 106 |
| `CDM` | 69 | 69 | 80 | 93 |
| `SAF` | 52 | 128 | 53 | 116 |
| `COP` | – | 142 | – | 16 |
| `STAT` | 15 | 68 | 44 | 91 |
| `REG` | 100 | 69 | 100 | 125 |
| `ERW` | 93 | 55 | 90 | 74 |
| `COM` | 109 | 22 | 108 | 20 |
| `PM` | 24 | 23 | 24 | 6 |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).