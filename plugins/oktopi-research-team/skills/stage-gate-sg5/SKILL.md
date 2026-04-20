---
name: stage-gate-sg5
description: Goal and readiness criteria for Oktopi stage-gate SG5: First-in-Human (FIH) Clinical Program Initiation. Trigger when assessing PDP readiness to exit SG5.
---

# Stage Gate SG5: First-in-Human (FIH) Clinical Program Initiation

**Goal.** Open IND, activate sites, dose the first subject safely and collect data suitable for dose-escalation and early PK/PD decisions.

**Primary focus areas.** IND clearance, site activation, FPFV safety, dose-escalation readiness

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG5` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG5` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG5` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 58 | 87 | 60 | 48 |
| `PT` | 60 | 81 | 65 | 120 |
| `TM` | 68 | 89 | 69 | 25 |
| `CP` | 53 | 39 | 62 | 59 |
| `CDM` | 62 | 56 | 67 | 52 |
| `SAF` | 40 | 102 | 40 | 21 |
| `COP` | – | 141 | – | – |
| `STAT` | 34 | 39 | 33 | 11 |
| `REG` | 38 | 26 | 38 | 71 |
| `ERW` | – | – | – | – |
| `COM` | 19 | – | 21 | 2 |
| `PM` | 18 | 17 | 18 | – |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).