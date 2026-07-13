---
name: setup
description: Initialize or upgrade a Git-native OKF second-brain repository for governed knowledge maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(mv *), Bash(mkdir *), Bash(git mv *)
---

# Setup Second Brain

Initialize the current directory as a governed OKF knowledge repository without overwriting existing user content. Obsidian is optional; do not require a `.obsidian/` directory.

Materialize the templates bundled under `${CLAUDE_PLUGIN_ROOT}/templates/vault/`, including `.gitkeep` placeholders (`raw/assets`, knowledge role dirs, `governance/reports`, `governance/proposals`, `output`). Creating a missing empty `raw/**/.gitkeep` is allowed scaffolding; never overwrite or edit source files under `raw/`.

## Required template paths

- `AGENTS.md`, `CLAUDE.md`
- `governance/{schema,ontology,policies,quality-rubric,source-ledger,automation-state}.md`
- `knowledge/index.md` (may include `okf_version: "0.1"`), `knowledge/log.md`
- `.cursor/rules/*.mdc`
- directory `.gitkeep` placeholders under the template tree

## Legacy migration (`wiki/` / `meta/`)

If `wiki/` or `meta/` exists and the OKF layout is missing or incomplete:

1. Rename `wiki/` → `knowledge/` when `knowledge/` does not already exist with user content; if both exist, report a conflict and do not clobber.
2. Rename `meta/` → `governance/` with the same conflict rule.
3. `Grep` for `\[\[` and only edit pages with hits: rewrite unambiguous wikilinks to Markdown per `governance/schema.md`; leave ambiguous targets as review notes.
4. `Grep` for legacy closed frontmatter `type: source|entity|concept|synthesis` and only edit matching pages: map to `knowledge_role` + open OKF `type` per schema; preserve unknown keys; set `timestamp` from `updated` when present.
5. Update path references in newly created or explicitly migrated contract/ledger files only; never overwrite divergent user governance without listing a conflict.

## Write rules

Before writing, inspect each target. Preserve existing content and report conflicts instead of replacing it. Ensure `CLAUDE.md` imports `AGENTS.md`.

Finish with a manifest of **created**, **migrated**, **preserved**, and **review-required** / conflict files. Mention that Obsidian users may disable “Use [[Wikilinks]]” so the editor emits Markdown links compatible with OKF.
