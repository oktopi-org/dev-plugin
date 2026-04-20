---
name: stage-gate-sg4
description: "Goal and readiness criteria for Oktopi stage-gate SG4: Pre-Clinical to FIH-Enabling (CMC, PK/PD, Tox Ready). Trigger when assessing PDP readiness to exit SG4."
---

# Stage Gate SG4: Pre-Clinical to FIH-Enabling (CMC, PK/PD, Tox Ready)

**Goal.** Complete IND-enabling package: GLP tox complete, CMC GMP drug product and IND Module 3, FIH protocol and starting dose justification.

**Primary focus areas.** GLP tox package, CMC GMP release, FIH protocol, starting dose

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG4` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG4` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG4` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 48 | 52 | 49 | 3 |
| `PT` | 102 | 120 | 107 | 23 |
| `TM` | 72 | 41 | 73 | 3 |
| `CP` | 42 | 9 | 42 | – |
| `CDM` | 37 | 6 | 35 | 11 |
| `SAF` | 23 | 6 | 18 | – |
| `COP` | – | 11 | – | – |
| `STAT` | 12 | – | 11 | – |
| `REG` | 33 | 18 | 33 | 34 |
| `ERW` | – | – | – | – |
| `COM` | 11 | – | 11 | – |
| `PM` | 18 | – | 18 | – |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).