# Second Brain Plugin

Claude Code and Cursor plugins for maintaining a **Git-native Open Knowledge Format (OKF)** knowledge repository—with governed provenance, verification, and automation.

This repository is a plugin monorepo. The primary plugin is [`second-brain`](plugins/second-brain/).

## Available plugins

| Plugin | Platforms | Description |
| --- | --- | --- |
| [`second-brain`](plugins/second-brain/README.md) | Claude Code, Cursor | Governed OKF knowledge workflows (setup, ingest, query, synthesize, lint, repair, maintain, status) |

## Installation (Claude Code)

Install into **project scope** so vault hooks only load in repositories that use this plugin:

```bash
/plugin marketplace add yu-iskw/second-brain-plugin
/plugin install second-brain@second-brain-plugin --scope project
```

Equivalent CLI form:

```bash
claude plugin install --scope project second-brain@second-brain-plugin
```

Then run `/second-brain:setup` from the repository root.

Full usage, safety model, and Obsidian notes: **[plugins/second-brain/README.md](plugins/second-brain/README.md)**.

### Cursor

`second-brain` also ships a Cursor manifest (`.cursor-plugin/`). Prefer project-local or team marketplace install so vault hooks stay scoped to repositories that use the plugin.

## Commands

- `/second-brain:setup`
- `/second-brain:ingest`
- `/second-brain:query`
- `/second-brain:synthesize`
- `/second-brain:lint`
- `/second-brain:repair`
- `/second-brain:maintain`
- `/second-brain:status`

## Repository layout

```text
.
├── plugins/
│   └── second-brain/            # OKF knowledge-management plugin
│       ├── .claude-plugin/      # Claude Code manifest
│       ├── .cursor-plugin/      # Cursor manifest
│       ├── agents/              # Role-separated subagents
│       ├── skills/              # Workflow skills
│       ├── hooks/               # Event hooks
│       ├── templates/           # Vault + automation templates
│       └── README.md            # End-user plugin docs
├── .claude-plugin/              # Claude marketplace catalog
├── .cursor-plugin/              # Cursor marketplace catalog
├── .codex-plugin/               # Codex marketplace catalog
├── integration_tests/           # Shared plugin smoke tests
├── .github/workflows/           # CI (lint + integration tests)
├── Makefile
├── CONTRIBUTING.md              # Developer guide
└── README.md
```

## Contributing

Want to change plugins, CI, or docs? See **[CONTRIBUTING.md](CONTRIBUTING.md)** for prerequisites, local checks, and how to add a plugin.

## License

Apache License 2.0. See [`LICENSE`](LICENSE).
