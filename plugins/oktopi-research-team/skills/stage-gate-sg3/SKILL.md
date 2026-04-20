---
name: stage-gate-sg3
description: "Goal and readiness criteria for Oktopi stage-gate SG3: Clinical Candidate Selection / IND-Enabling Entry. Trigger when assessing PDP readiness to exit SG3."
---

# Stage Gate SG3: Clinical Candidate Selection / IND-Enabling Entry

**Goal.** Confirm a single clinical candidate with an approved IND-enabling plan across CMC, tox, PK/PD, and clinical design.

**Primary focus areas.** candidate selection data, IND-enabling study plan, CMC readiness for GLP/GMP, target product profile draft

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG3` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG3` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG3` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 14 | 3 | 14 | – |
| `PT` | 44 | 24 | 43 | – |
| `TM` | 36 | 3 | 37 | – |
| `CP` | 6 | – | 5 | – |
| `CDM` | 17 | – | 17 | 3 |
| `SAF` | – | – | – | – |
| `COP` | – | – | – | – |
| `STAT` | – | – | – | – |
| `REG` | 13 | – | 13 | 12 |
| `ERW` | 23 | – | 23 | – |
| `COM` | 19 | – | 19 | – |
| `PM` | 10 | – | 10 | – |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).