---
name: setup
description: Initialize or upgrade an Obsidian vault for governed second-brain maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Setup Second Brain

Initialize the current directory as a vault without overwriting existing user content. This is a first-time vault setup / governance initialization when creating missing governance files.

Materialize the templates bundled under `${CLAUDE_PLUGIN_ROOT}/templates/vault/`, including `.gitkeep` placeholders that create empty directories (`raw/assets`, wiki page-type dirs, `meta/reports`, `meta/proposals`, `output`). Creating a missing empty `raw/**/.gitkeep` is allowed scaffolding; never overwrite or edit source files under `raw/`.

Required template paths include:

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
- directory `.gitkeep` placeholders under the template tree

Before writing, inspect each target. Preserve existing content and report conflicts instead of replacing it. Ensure `CLAUDE.md` imports `AGENTS.md`. Finish with a manifest of created, preserved, and review-required files.
