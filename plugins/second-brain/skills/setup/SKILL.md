---
name: setup
description: Initialize or upgrade an Obsidian vault for governed second-brain maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Setup Second Brain

Initialize the current directory as a vault without overwriting existing user content. This is a first-time vault setup / governance initialization when creating missing governance files.

Create missing directories by writing placeholder `.gitkeep` files when no other file exists yet:

- `raw/assets/.gitkeep`
- `wiki/sources/.gitkeep`
- `wiki/entities/.gitkeep`
- `wiki/concepts/.gitkeep`
- `wiki/synthesis/.gitkeep`
- `meta/reports/.gitkeep`
- `meta/proposals/.gitkeep`
- `output/.gitkeep`

Materialize the templates bundled under `${CLAUDE_PLUGIN_ROOT}/templates/vault/` (including matching `.gitkeep` placeholders when present):

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

Before writing, inspect each target. Preserve existing content and report conflicts instead of replacing it. Ensure `CLAUDE.md` imports `AGENTS.md`. Finish with a manifest of created, preserved, and review-required files.
