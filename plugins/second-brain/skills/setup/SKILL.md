---
name: setup
description: Initialize or upgrade a Git-native OKF second-brain repository for governed knowledge maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(mv *), Bash(mkdir *), Bash(git mv *)
---

# Setup Second Brain

Initialize the current directory as a governed OKF knowledge repository without overwriting existing user content. Obsidian is optional; do not require a `.obsidian/` directory.

Materialize the templates bundled under `${CLAUDE_PLUGIN_ROOT}/templates/vault/`, including `.gitkeep` placeholders that create empty directories (`raw/assets`, knowledge role dirs, `governance/reports`, `governance/proposals`, `output`). Creating a missing empty `raw/**/.gitkeep` is allowed scaffolding; never overwrite or edit source files under `raw/`.

## Required template paths

- `AGENTS.md`
- `CLAUDE.md`
- `governance/schema.md`
- `governance/ontology.md`
- `governance/policies.md`
- `governance/quality-rubric.md`
- `governance/source-ledger.md`
- `governance/automation-state.md`
- `knowledge/index.md` (may include `okf_version: "0.1"` frontmatter)
- `knowledge/log.md`
- `.cursor/rules/*.mdc`
- directory `.gitkeep` placeholders under the template tree

## Legacy migration (`wiki/` / `meta/`)

If `wiki/` or `meta/` exists and the OKF layout is missing or incomplete:

1. Rename `wiki/` → `knowledge/` when `knowledge/` does not already exist with user content; if both exist, report a conflict and do not clobber.
2. Rename `meta/` → `governance/` with the same conflict rule.
3. Rewrite internal Obsidian `[[wikilinks]]` in migrated knowledge pages to canonical Markdown links (prefer bundle-absolute `/path.md` under `knowledge/`) when the target is unambiguous; otherwise leave a review note.
4. Map legacy closed frontmatter `type: source|entity|concept|synthesis` to `knowledge_role` plus open OKF `type` (`Source`/`Entity`/`Concept`/`Synthesis` defaults). Preserve all unknown keys. Set `timestamp` from `updated` when present.
5. Update path references in `AGENTS.md`, ledgers, and logs from `wiki/`/`meta/` to `knowledge/`/`governance/` only when those files are being created or explicitly migrated; never overwrite divergent user governance without listing a conflict.

## Write rules

Before writing, inspect each target. Preserve existing content and report conflicts instead of replacing it. Ensure `CLAUDE.md` imports `AGENTS.md`.

Finish with a manifest of **created**, **migrated**, **preserved**, and **review-required** / conflict files. Mention that Obsidian users may disable “Use [[Wikilinks]]” so the editor emits Markdown links compatible with OKF.
