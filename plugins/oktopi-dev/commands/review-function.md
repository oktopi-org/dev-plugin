---
name: review-function
description: Run a single-function PDP gap review using the matching Oktopi function-reviewer agent
argument-hint: <function-code-or-slug> <SG1..SG9> <SR|OE|DD|RS> [small-molecule|biologics] [document]
---

# Review a PDP for a single function

Arguments (positional):

1. `function` — either a function code (`CMC`, `COM`, `STAT`, ...) or a slug (`commercial`, `biostatistics`, ...). See `data/functions.json`.
2. `stage_gate` — `SG1`..`SG9`
3. `mode` — `SR`, `OE`, `DD`, or `RS`
4. `modality` *(optional, default `small-molecule`)*
5. `document` *(optional)* — path or URL

## Workflow

1. Resolve the function slug via `data/functions.json` (fall back to the slug map in `scripts/build_taxonomy_data.py`).
2. Dispatch the `<slug>-reviewer` agent with the stage-gate, mode, modality, and document.
3. Relay the agent's structured report back to the user verbatim.
