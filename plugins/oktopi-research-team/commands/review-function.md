---
name: review-function
description: Dispatch a single Oktopi function reviewer agent to review a PDP from that function's perspective
argument-hint: <function-code-or-slug> <SG1..SG9> <SR|OE|DD|RS> [small-molecule|biologics] [document]
---

# Review a PDP for a single function

Dispatch the matching function reviewer agent. Use this when the user wants a focused read from one function (e.g. "just give me the Commercial view on SG6"), as opposed to a full multi-function stage-gate review.

Arguments (positional):

1. `function` — either a function code (`CMC`, `COM`, `STAT`, ...) or a slug (`commercial`, `biostatistics`, `pharmtox`, ...). See `data/functions.json`.
2. `stage_gate` — `SG1..SG9`
3. `mode` — `SR | OE | DD | RS`
4. `modality` *(optional, default `small-molecule`)*
5. `document` *(optional)* — path or URL

## Workflow

1. Resolve the slug from `data/functions.json` if the user passed a code.
2. Dispatch the `<slug>-reviewer` subagent with the stage-gate, mode, modality, and document.
3. Relay the agent's structured JSON verdict back to the user without re-synthesizing — it is the contract the `pdp-reviewer` orchestrator depends on.
