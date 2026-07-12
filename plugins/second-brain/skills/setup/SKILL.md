---
name: setup
description: Initialize or upgrade an Obsidian vault for governed second-brain maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Setup Second Brain

Initialize the current directory as a vault without overwriting existing user content.

Create missing directories: `raw/assets`, `wiki/sources`, `wiki/entities`, `wiki/concepts`, `wiki/synthesis`, `meta/reports`, `meta/proposals`, and `output`.

Materialize the templates bundled under `${CLAUDE_PLUGIN_ROOT}/templates/vault/`:

- `AGENTS.md`
- `CLAUDE.md`
- `meta/schema.md`
- `meta/ontology.md`
- `meta/policies.md`
- `meta/quality-rubric.md`
- `meta/source-ledger.md`
- `meta/automation-state.md`
- `wiki/index.md`
- `wiki/log.md`
- `.cursor/rules/*.mdc`
- `.cursor/agents/*.md`

Before writing, inspect each target. Preserve existing content and report conflicts instead of replacing it. Ensure `CLAUDE.md` imports `AGENTS.md`. Finish with a manifest of created, preserved, and review-required files.
