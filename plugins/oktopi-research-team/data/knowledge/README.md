# Per-function knowledge base

Add function-specific reference material (SOPs, guidelines, precedent reviews, playbooks, template questionnaires) under `<FUNCTION_CODE>/`.

Each function's reviewer agent is told to load this folder alongside the formal Oktopi rubric. Keep files in markdown or JSON for easy parsing.

Suggested structure per function:

```
knowledge/<CODE>/
├── playbooks/      # Worked examples the reviewer can cite
├── sops/           # Internal SOPs and checklists
├── guidelines/     # Regulatory / industry guidelines summaries
└── tools.md        # Notes on external tools / MCP servers this function uses
```
