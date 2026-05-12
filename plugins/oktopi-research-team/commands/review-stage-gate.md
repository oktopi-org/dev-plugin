---
description: Review a PDP against an Oktopi stage-gate by dispatching the pdp-reviewer orchestrator
argument-hint: <SG1..SG9> <SR|OE|DD|RS> [small-molecule|biologics] [path-to-document]
---

# Review a PDP against an Oktopi stage-gate

Invoke the **pdp-reviewer** orchestrator agent. It fans out to the relevant function reviewers (using the multi-agent research pattern — parallel subagents, structured reports, synthesized verdict) and returns a gate-readiness report.

Arguments (positional):

1. `stage_gate` — one of `SG1 SG2 SG3 SG4 SG5 SG6 SG7 SG8 SG9`
2. `mode` — one of `SR | OE | DD | RS`
3. `modality` *(optional, default `small-molecule`)* — `small-molecule | biologics`
4. `document` *(optional)* — path or URL to the PDP / data room

Your job: pass these through to `pdp-reviewer`. Do not review the PDP yourself — the orchestrator owns the workflow, parallelism, and reconciliation.

If the user omits required arguments, ask once for them and then invoke.
