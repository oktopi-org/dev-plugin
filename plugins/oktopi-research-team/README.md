# oktopi-research-team plugin

PDP (Product Development Plan) gap-analysis for Claude Code, designed as an
agentic, multi-agent review system (inspired by Anthropic's
[multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system))
and grounded in the shared Oktopi [Taxonomy-config](https://github.com/oktopi-org/Taxonomy-config).

## Architecture

```
           ┌──────────────────────────┐
           │      pdp-reviewer        │   ← orchestrator (Lead Reviewer)
           │  scope → dispatch → sync │     model: opus
           └─────────────┬────────────┘
                         │  Task tool, parallel fan-out
     ┌──────────┬────────┼────────┬──────────────────┐
     ▼          ▼        ▼        ▼                  ▼
  cmc-rev   pharm-tox  …      commercial-rev     pm-rev    (12 function reviewers — sonnet)
     │          │        │        │                  │
     └──────────┴────────┴────────┴──────────────────┘
                         │
                         ▼
              structured JSON verdicts
                         │
                         ▼
              gate-readiness report
```

Each reviewer:
- **Embodies the role's goal** (seasoned pharma function lead persona)
- **Anchors on the Oktopi rubric** via `data/questions/<modality>/<FN>.json`
- **Asks adaptive follow-ups** when the rubric doesn't cover a novel risk
- **Returns a structured JSON** the orchestrator can reconcile

## What's inside

```
plugins/oktopi-research-team/
├── agents/                                 # 12 function reviewers + 1 orchestrator
│   ├── pdp-reviewer.md                     # Lead Reviewer (orchestrator)
│   ├── cmc-reviewer.md
│   ├── commercial-reviewer.md
│   └── ... (10 more functions)
├── skills/
│   ├── stage-gate-sg1/ … stage-gate-sg9/   # 9 gate-goal skills (concise)
│   └── function-<slug>/                    # 12 function-mandate skills
├── commands/
│   ├── review-stage-gate.md                # /review-stage-gate
│   └── review-function.md                  # /review-function
├── data/
│   ├── functions.json                      # role + mission + mandate per function
│   ├── stage-gates.json                    # SG1..SG9 with goal + focus
│   ├── stage-gate-index.json               # counts per (SG, mode, function) + domains
│   ├── modes.json                          # SR / OE / DD / RS
│   ├── heatmap/<modality>.json             # question → {mode → {sg → priority}}
│   └── questions/<modality>/<FN>.json      # 1,492 questions with priorities + rubric
└── scripts/
    └── build_taxonomy_data.py              # regenerate everything from Taxonomy-config
```

## Why this design

- **Auto-routing by natural language.** Every agent and skill description lists the user phrases that should trigger it (`"Use PROACTIVELY when the user asks about: GMP manufacturing, tech transfer, or process validation..."`). Claude matches the user's question against these triggers and auto-invokes the right specialist — no explicit `/command` needed. A top-level `oktopi-research-team` router skill catches any pharma dev question and delegates.
- **Agents are goal-embodied, not question-parroting.** Each reviewer knows *why* they exist (their mission) and what they own (their mandate). The 1,492-question rubric is their *floor*, not their ceiling — they're explicitly instructed to add adaptive questions when a novel modality or fresh regulatory signal demands it.
- **Orchestrator owns parallelism and reconciliation.** Like a Lead Researcher, `pdp-reviewer` scopes the work, dispatches subagents concurrently, and synthesizes one gate-readiness report with cross-functional risk clustering.
- **Skills describe intent, not data.** Stage-gate and function skills are concise goal statements (< 10 KB each) that trigger naturally when the user mentions a gate or function. Question-level data lives in JSON that agents load on demand.
- **Every finding is citable.** Question IDs (`COM5`, `BBSTAT18`, etc.) link back to the Oktopi Expert Toolkit rubrics; adaptive questions are tagged `[adaptive]` with a rationale.

## Expanding an agent's tooling and knowledge

Each reviewer is designed to grow — add reference material and tools without touching the build script:

- **Per-function knowledge** lives under [`data/knowledge/<CODE>/`](data/knowledge/) (one directory per function, scaffolded on build). Drop SOPs, playbooks, guideline summaries, template questionnaires in markdown or JSON. The matching reviewer is instructed to scan this folder alongside the rubric.
- **External tools (MCP)**: add servers to the plugin's `.mcp.json` (e.g. ClinicalTrials.gov, PubMed, an internal CMC database). Then extend the `tools:` frontmatter in the specific `<slug>-reviewer.md` agent to grant access (e.g. `tools: Read, Grep, Glob, mcp__pubmed__search`).
- **Sub-specialists**: spawn a narrower agent under `agents/<slug>-<subspeciality>.md` (e.g. `commercial-hta-specialist`). Reference it from the parent reviewer's workflow.
- **Trigger tuning**: if a function should catch more phrases, edit that function's `triggers:` list in `build_taxonomy_data.py` and rerun the script — descriptions and the router skill regenerate automatically.

## Usage

```text
/review-stage-gate SG5 OE small-molecule ~/Desktop/acme-pdp.pdf
```

The command hands off to `pdp-reviewer`, which:
1. Loads `stage-gate-index.json` to see which functions carry Critical question load at SG5 × OE
2. Dispatches those function reviewers in parallel
3. Each reviewer loads its question bank, filters on Critical at SG5/OE, evaluates evidence, and returns structured JSON
4. Orchestrator reconciles into one readiness report with cross-functional risk clusters

For a single-function pass:

```text
/review-function commercial SG6 DD biologics ~/Desktop/acme-dataroom/
```

## Regenerating data

```bash
git clone https://github.com/oktopi-org/Taxonomy-config.git
python3 plugins/oktopi-research-team/scripts/build_taxonomy_data.py \
    --taxonomy ./Taxonomy-config
```

Requires Python 3.10+ and `openpyxl`. The script regenerates:

- All 13 agent markdown files (12 reviewers + orchestrator)
- All 22 skill files (9 stage-gate + 12 function + 1 top-level router)
- All JSON data under `data/`, including scaffolded `data/knowledge/<CODE>/` directories

## Extending

- **Change a role's mission or mandate** → edit `FUNCTIONS` in `build_taxonomy_data.py` and rebuild.
- **Tune the orchestrator** → edit `render_orchestrator_agent()`.
- **Add a new function** → add a `FUNCTIONS` entry + `FUNCTION_SLUG` + rubric file mapping, and the script will generate the agent, skill, and question JSON.
