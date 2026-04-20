# oktopi-dev plugin

PDP (Product Development Plan) gap-analysis toolkit for Claude Code. Wraps the
Oktopi [Taxonomy-config](https://github.com/oktopi-org/Taxonomy-config) so that
Claude agents can review a PDP against the 9 Oktopi stage-gates across 12
functional areas, in 4 assessment modes (Strategic Readiness, Operational
Execution, Due Diligence, Regulatory Submission), for both small-molecule and
biologics modalities.

## What's inside

```
plugins/oktopi-dev/
├── agents/                       # 12 function reviewer subagents
│   ├── cmc-reviewer.md
│   ├── commercial-reviewer.md
│   ├── biostatistics-reviewer.md
│   └── ...
├── skills/                       # 9 stage-gate goal skills
│   ├── stage-gate-sg1/SKILL.md
│   ├── stage-gate-sg2/SKILL.md
│   └── ...
├── commands/
│   ├── review-stage-gate.md      # /review-stage-gate
│   └── review-function.md        # /review-function
├── data/
│   ├── functions.json            # 12 functions with SM + biologics codes
│   ├── stage-gates.json          # SG1..SG9 with goal + focus
│   ├── modes.json                # SR / OE / DD / RS
│   ├── heatmap/                  # question -> {mode -> {sg -> priority}}
│   │   ├── small-molecule.json
│   │   └── biologics.json
│   └── questions/                # per-function question banks
│       ├── small-molecule/<FN>.json  (12 files, 613 total questions)
│       └── biologics/<FN>.json       (12 files, 879 total questions)
└── scripts/
    └── build_taxonomy_data.py    # regenerate data + agents + skills
```

## How the taxonomy maps to components

- **Functions → agents.** Every functional area (CMC, Pharm-Tox, Translational
  Medicine, Clinical Pharmacology, Clinical Development/Medical, Clinical
  Safety, Clinical Operations, Biostatistics, Regulatory Affairs, Epi & RWE,
  Commercial, Project Management) gets its own reviewer agent that knows its
  full question bank and how those questions are prioritized for each stage-gate
  and mode.
- **Stage-gates → skills.** SG1–SG9 each get a skill file that states the
  gate's goal and lists the Critical questions (per mode, per function) that
  must be answered before the gate can be cleared.
- **Modes** (`SR`, `OE`, `DD`, `RS`) control which priority matrix is used —
  the same question is rated Critical / Expected / Check / Other per mode.

## Typical usage

```text
/review-stage-gate SG5 OE small-molecule ~/Desktop/acme-pdp.pdf
```

The command loads `skills/stage-gate-sg5/SKILL.md`, dispatches each function
reviewer in parallel, and aggregates the results into a single SG5 readiness
report.

For a single function:

```text
/review-function commercial SG6 DD biologics ~/Desktop/acme-dataroom/
```

## Regenerating data

The agents, skills, and JSON data are all generated from the upstream
`Taxonomy-config` repo. To refresh after the taxonomy changes:

```bash
# Clone the taxonomy repo next to this one (sibling directory)
git clone https://github.com/oktopi-org/Taxonomy-config.git

python3 plugins/oktopi-dev/scripts/build_taxonomy_data.py \
    --taxonomy ../Taxonomy-config
```

Requirements: Python 3.10+ and `openpyxl`.
