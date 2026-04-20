---
name: stage-gate-sg6
description: "Goal and readiness criteria for Oktopi stage-gate SG6: Proof of Concept (POC) & Phase 2 Readiness. Trigger when assessing PDP readiness to exit SG6."
---

# Stage Gate SG6: Proof of Concept (POC) & Phase 2 Readiness

**Goal.** Demonstrate clinical proof of concept and confirm Phase 2 design, dose, population, endpoints, and operational feasibility.

**Primary focus areas.** POC criteria met, Phase 2 protocol, biomarker strategy, scale-up CMC

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG6` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG6` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG6` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 79 | 99 | 81 | 102 |
| `PT` | 29 | 38 | 51 | 82 |
| `TM` | 77 | 100 | 77 | 74 |
| `CP` | 86 | 56 | 95 | 98 |
| `CDM` | 75 | 62 | 81 | 75 |
| `SAF` | 43 | 104 | 45 | 56 |
| `COP` | – | 142 | – | 1 |
| `STAT` | 30 | 61 | 43 | 59 |
| `REG` | 66 | 31 | 66 | 108 |
| `ERW` | 28 | 29 | 27 | 7 |
| `COM` | 73 | – | 71 | 3 |
| `PM` | 24 | 23 | 24 | – |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).