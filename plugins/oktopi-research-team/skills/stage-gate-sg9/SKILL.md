---
name: stage-gate-sg9
description: Goal and readiness criteria for Oktopi stage-gate SG9: Launch & Post-Market Lifecycle Management. Trigger when assessing PDP readiness to exit SG9.
---

# Stage Gate SG9: Launch & Post-Market Lifecycle Management

**Goal.** Execute a compliant launch and sustain post-market obligations, lifecycle planning, and RWE/safety monitoring.

**Primary focus areas.** PSUR/PBRER, REMS/RMP, LCM indications, RWE commitments

## How to use this skill

1. Invoke the `pdp-reviewer` agent with stage-gate `SG9` and the mode (`SR|OE|DD|RS`).
2. The orchestrator dispatches the relevant function reviewers in parallel, each filtering on Critical questions at `SG9` in that mode.
3. Each reviewer returns a structured JSON verdict; the orchestrator consolidates into a gate-readiness report.

## Function load at this gate (Critical question counts)

The table below shows how many Critical questions each function carries at `SG9` per mode. Use it to prioritize which reviewers to spawn — functions with zero Critical questions can be deprioritized or run on a lighter cadence.

| Function | SR | OE | DD | RS |
| --- | ---: | ---: | ---: | ---: |
| `CMC` | 2 | 2 | 2 | 2 |
| `PT` | – | – | – | – |
| `TM` | 5 | 4 | 4 | – |
| `CP` | – | – | – | – |
| `CDM` | 26 | 10 | 26 | 20 |
| `SAF` | 31 | 128 | 31 | 108 |
| `COP` | – | 2 | – | – |
| `STAT` | – | – | – | – |
| `REG` | 37 | 33 | 37 | 43 |
| `ERW` | 72 | 42 | 70 | 70 |
| `COM` | 104 | 26 | 103 | 17 |
| `PM` | 6 | 6 | 6 | 6 |

## Reference data

- `data/stage-gates.json` — goal and focus for every stage-gate
- `data/stage-gate-index.json` — Critical question counts per (SG, mode, function) with inquiry domains
- `data/questions/<modality>/<FN>.json` — the full question bank per function (reviewer agents load this)
- `data/heatmap/<modality>.json` — raw priority map `{question_id: {mode: {sg: label}}}`

## Related

Function-specific mandates are in the per-function skills (`skills/function-<slug>/SKILL.md`).