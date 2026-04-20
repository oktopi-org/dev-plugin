# Oktopi Dev — Claude Code Marketplace

A Claude Code plugin marketplace for Oktopi development workflows.

## Installation

Add this marketplace in Claude Code:

```
/plugin marketplace add oktopi-org/dev-plugin
```

Then install plugins from it:

```
/plugin install oktopi-dev@oktopi-dev
```

## Plugins

### [`oktopi-dev`](plugins/oktopi-dev/)

PDP gap-analysis toolkit derived from [Taxonomy-config](https://github.com/oktopi-org/Taxonomy-config):

- **12 function reviewer agents** — one per functional area (CMC, Commercial,
  Biostatistics, Regulatory, etc.) covering both small-molecule and biologics.
- **9 stage-gate skills** — SG1–SG9, each with the gate goal and the Critical
  questions per mode (Strategic Readiness / Operational Execution / Due
  Diligence / Regulatory Submission).
- **2 slash commands** — `/review-stage-gate` (multi-function) and
  `/review-function` (single function).
- **1,492 question bank** distilled into JSON data files the agents read at
  runtime.

See [plugins/oktopi-dev/README.md](plugins/oktopi-dev/README.md) for usage.

## Structure

```
dev-plugin/
├── .claude-plugin/
│   └── marketplace.json        # Marketplace manifest
└── plugins/
    └── oktopi-dev/
        ├── .claude-plugin/plugin.json
        ├── agents/             # 12 function reviewer agents
        ├── skills/             # 9 stage-gate SKILL.md files
        ├── commands/           # Slash commands
        ├── data/               # Generated taxonomy data
        └── scripts/            # Regeneration script
```

## Adding a New Plugin

1. Create a directory under `plugins/` (e.g. `plugins/my-plugin/`).
2. Add `.claude-plugin/plugin.json` with at least a `name` field.
3. Add component directories (`commands/`, `agents/`, `skills/`, `hooks/`) as needed.
4. Register the plugin in `.claude-plugin/marketplace.json` under the `plugins` array.

## References

- [Plugin marketplaces](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [Plugin reference](https://docs.claude.com/en/docs/claude-code/plugins-reference)
