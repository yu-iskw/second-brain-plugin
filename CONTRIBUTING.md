# Contributing

Thanks for contributing to this plugin monorepo. This guide is for developers working on plugins, CI, and repository tooling. End-user install and usage live in [`README.md`](README.md) and [`plugins/second-brain/README.md`](plugins/second-brain/README.md).

## Prerequisites

- `git`
- `docker`
- [`trunk`](https://trunk.io) CLI
- Optional: [`claude`](https://code.claude.com/docs/en/overview) CLI (`npm install -g @anthropic-ai/claude-code`) for full plugin loading and marketplace install checks

## Setup

1. Fork or branch from this repository.
2. Install Trunk:
   ```bash
   curl https://get.trunk.io -fsSL | bash
   ```
3. Verify tools:
   ```bash
   trunk --version
   docker --version
   ```

## Local checks

Run these before opening a pull request:

```bash
make format
make lint
make test-integration-docker
```

`make test-integration-docker` builds `integration_tests/Dockerfile` and runs the full smoke suite, including marketplace **add → install → list** for every plugin in `.claude-plugin/marketplace.json`.

You can also run scripts directly from the repo root:

| Command                                      | Purpose                                                               |
| -------------------------------------------- | --------------------------------------------------------------------- |
| `./integration_tests/run.sh`                 | Discover plugins under `plugins/` and run validation + loading checks |
| `./integration_tests/run.sh --verbose`       | Same with verbose output                                              |
| `./integration_tests/run.sh --manifest-only` | Manifest / structure checks only (Claude, Cursor, Codex)              |
| `./integration_tests/run.sh --skip-loading`  | Skip Claude CLI loading tests                                         |
| `./integration_tests/validate-manifest.sh`   | Claude `plugin.json` schema validation                                |
| `./integration_tests/test-plugin-install.sh` | Marketplace install test (requires Claude CLI)                        |

CI runs Trunk Check plus the integration suite (including a Docker install job). Local Docker smoke should match job `plugin-install-docker`.

## Repository structure

```text
plugins/<name>/
├── .claude-plugin/plugin.json   # Required for Claude Code
├── .cursor-plugin/plugin.json   # Optional: Cursor
├── .codex-plugin/plugin.json    # Optional: Codex
├── skills/<skill>/SKILL.md
├── agents/
├── hooks/hooks.json
├── commands/                    # Optional slash commands
├── rules/                       # Optional Cursor rules
├── .mcp.json / .lsp.json        # Optional Claude MCP/LSP wiring
└── README.md                    # End-user docs for the plugin
```

Root marketplace catalogs:

- `.claude-plugin/marketplace.json` — Claude Code
- `.cursor-plugin/marketplace.json` — Cursor
- `.codex-plugin/marketplace.json` — Codex (may have `"plugins": []` until a Codex-capable plugin with `.codex-plugin/plugin.json` is registered)

Integration tests auto-discover directories under `plugins/` that contain `.claude-plugin/`. Install tests install every entry listed in `.claude-plugin/marketplace.json`.

## Adding a new plugin

1. Create `plugins/<name>/` using the [standard plugin layout](https://code.claude.com/docs/en/plugins-reference#standard-plugin-layout).
2. Add a required Claude manifest at `plugins/<name>/.claude-plugin/plugin.json` (`name`, `version`, `description`).
3. Add components as needed:
   - **Skills** — `skills/<skill-name>/SKILL.md` (specific, testable instructions)
   - **Agents** — Markdown under `agents/` with front matter (`name`, `description`)
   - **Hooks** — `hooks/hooks.json` (valid, minimal JSON)
   - **Commands** — under `commands/` when you need explicit slash commands
4. For multi-platform support, add `.cursor-plugin/plugin.json` and/or `.codex-plugin/plugin.json` alongside `.claude-plugin/`. Shared `skills/` (and other root components) can be reused across platforms.
5. **Register the plugin** in the relevant marketplace file(s):
   - Always: `.claude-plugin/marketplace.json`
   - If Cursor-capable: `.cursor-plugin/marketplace.json`
   - If Codex-capable: `.codex-plugin/marketplace.json`
   - Include at least `name`, `source` (e.g. `./plugins/<name>`), `version`, `description`, and `repository`.
6. Add a plugin-level `README.md` with install and usage for end users.
7. Run `make format`, `make lint`, and `make test-integration-docker`.

Agent-assisted workflows (optional): see `.claude/skills/implement-plugin/SKILL.md`, platform-specific `implement-*-plugin` skills, and `.claude/skills/plugin-verification/SKILL.md`.

## Updating an existing plugin

- Keep changes scoped to one concern when possible.
- Update the plugin README when user-facing behavior or install steps change.
- Bump the plugin `version` in both the per-plugin manifest(s) and the matching marketplace entry when you cut a releasable change.
- Prefer small, reviewable commits.

## Pull request guidelines

1. Keep changes focused.
2. Update docs when behavior or structure changes.
3. Include test evidence in the PR description (commands run and outcomes).
4. Ensure CI passes (`trunk_check` and `integration_tests`).

## Commit guidelines

- Use clear, imperative commit messages.
- Prefer small commits that are easy to review.

## Reporting issues

Open an issue with:

- expected behavior
- actual behavior
- reproduction steps
- logs or screenshots when relevant
