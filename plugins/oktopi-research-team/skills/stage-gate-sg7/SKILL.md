---
name: stage-gate-sg7
description: "Goal and readiness criteria for Oktopi stage-gate SG7: Confirmatory & Phase 3 Readiness (Reg & Commercial aligned). Trigger when assessing PDP readiness to exit SG7."
---

# Stage Gate SG7: Confirmatory & Phase 3 Readiness (Reg & Commercial aligned)

**Goal.** Lock Phase 3 design with regulatory and commercial alignment; confirm CMC registration strategy and site/CRO readiness.

**Primary focus areas.** Phase 3 design, EoP2 alignment, registration CMC, TPP lock

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG7` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG7` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG7` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 73 | 100 | 82 | 118 |
| `PT` | 29 | 39 | 34 | 38 |
| `TM` | 59 | 100 | 59 | 75 |
| `CP` | 98 | 60 | 105 | 106 |
| `CDM` | 83 | 62 | 90 | 88 |
| `SAF` | 67 | 128 | 69 | 116 |
| `COP` | – | 142 | – | 12 |
| `STAT` | 21 | 66 | 47 | 89 |
| `REG` | 100 | 36 | 100 | 123 |
| `ERW` | 76 | 38 | 73 | 22 |
| `COM` | 111 | 2 | 110 | 20 |
| `PM` | 24 | 23 | 24 | 6 |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).