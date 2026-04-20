---
name: stage-gate-sg1
description: Goal and readiness criteria for Oktopi stage-gate SG1: Initiate Discovery Program & Target Identification. Trigger when assessing PDP readiness to exit SG1.
---

# Stage Gate SG1: Initiate Discovery Program & Target Identification

**Goal.** Validate a biologically credible target, a defensible rationale, and a screening plan that can yield testable hypotheses.

**Primary focus areas.** target validation, MoA rationale, IP freedom-to-operate, discovery plan & budget

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG1` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG1` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG1` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 4 | – | – | – |
| `PT` | 14 | – | 14 | – |
| `TM` | 3 | – | 3 | – |
| `CP` | 3 | – | – | – |
| `CDM` | 11 | – | 9 | – |
| `SAF` | – | – | – | – |
| `COP` | – | – | – | – |
| `STAT` | – | – | – | – |
| `REG` | 10 | – | 10 | – |
| `ERW` | 8 | – | 8 | – |
| `COM` | 17 | – | 17 | – |
| `PM` | – | – | – | – |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).