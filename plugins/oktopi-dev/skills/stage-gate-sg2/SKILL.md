---
name: stage-gate-sg2
description: Goal and readiness criteria for Oktopi stage-gate SG2: Lead Nomination / Early Optimization. Trigger when assessing PDP readiness to exit SG2.
---

# Stage Gate SG2: Lead Nomination / Early Optimization

**Goal.** Nominate a lead series with acceptable developability signals and a clear optimization plan to reach clinical candidate criteria.

**Primary focus areas.** lead criteria met, DMPK/tox early signals, scaffold IP, formulation feasibility

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG2` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG2` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG2` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 5 | – | 1 | – |
| `PT` | 19 | – | 18 | – |
| `TM` | 20 | – | 20 | – |
| `CP` | 3 | – | – | – |
| `CDM` | 11 | – | 9 | – |
| `SAF` | – | – | – | – |
| `COP` | – | – | – | – |
| `STAT` | – | – | – | – |
| `REG` | 9 | – | 9 | – |
| `ERW` | 18 | – | 18 | – |
| `COM` | 24 | – | 24 | – |
| `PM` | – | – | – | – |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).