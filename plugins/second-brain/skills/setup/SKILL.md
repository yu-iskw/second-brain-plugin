---
name: setup
description: Initialize or upgrade a Git-native OKF second-brain repository for governed knowledge maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git mv wiki knowledge), Bash(git mv meta governance), Bash(mv wiki knowledge), Bash(mv meta governance), Bash(mkdir *)
---

# Setup Second Brain

Initialize the current directory as a governed OKF knowledge repository without overwriting existing user content. Obsidian is optional; do not require a `.obsidian/` directory.

Materialize the templates bundled under `${CLAUDE_PLUGIN_ROOT}/templates/vault/`, including `.gitkeep` placeholders (`raw/assets`, knowledge role dirs, `governance/reports`, `governance/proposals`, `output`). Creating a missing empty `raw/**/.gitkeep` is allowed scaffolding; never overwrite or edit source files under `raw/`.

Shell renames are limited to `wiki`→`knowledge` and `meta`→`governance` only. Do not `mv`/`git mv` other paths.

## Required template paths

- `AGENTS.md`, `CLAUDE.md`
- `governance/{schema,ontology,policies,quality-rubric,source-ledger,automation-state}.md`
- `knowledge/index.md` (may include `okf_version: "0.1"`), `knowledge/log.md`
- `.cursor/rules/*.mdc`
- directory `.gitkeep` placeholders under the template tree

## Legacy path migration (`wiki/` / `meta/`)

If `wiki/` or `meta/` exists and the OKF layout is missing or incomplete:

1. Rename `wiki/` → `knowledge/` when `knowledge/` does not already exist with user content; if both exist, report a conflict and do not clobber.
2. Rename `meta/` → `governance/` with the same conflict rule.
3. `Grep` for `\[\[` under `knowledge/` and only edit pages with hits: rewrite unambiguous wikilinks to Markdown per `governance/schema.md`; leave ambiguous targets as review notes.
4. `Grep` for legacy closed frontmatter `type: source|entity|concept|synthesis` and only edit matching pages: map to `knowledge_role` + open OKF `type` per schema/ontology; preserve unknown keys; set `timestamp` from `updated` when present.

## Governance content upgrade (required for OKF)

Path rename alone is not enough. Detect **pre-OKF governance** when any of these hold for `governance/schema.md` (or legacy `meta/schema.md` before rename):

- missing the string `okf-core` or `knowledge_role`
- mandates Obsidian `[[wikilinks]]` as the canonical link form
- uses a closed `type: source | entity | concept | synthesis` enum without `knowledge_role`

When pre-OKF (or the OKF governance file is missing):

1. Backup the existing file under `governance/proposals/legacy-<name>-backup.md` (create `proposals/` if needed). Do the same for `ontology.md`, `policies.md`, and root `AGENTS.md` when they still describe `wiki/**` / `meta/**` or lack OKF ownership boundaries.
2. Materialize the current plugin templates for `governance/schema.md`, `governance/ontology.md`, `governance/policies.md`, and `AGENTS.md` (and `quality-rubric.md` when missing).
3. Mark the upgrade as **migrated** with **review-required** so humans can re-apply local customizations from the backups.

If both a customized OKF-era file and a template conflict in substance, preserve the user file, write the template beside it as `*.okf-template.md` under `governance/proposals/`, and list a conflict—do not clobber OKF-conformant user governance.

## Write rules

Before writing, inspect each target. Preserve existing OKF-conformant content and report conflicts instead of replacing it. Ensure `CLAUDE.md` imports `AGENTS.md`.

Finish with a manifest of **created**, **migrated**, **preserved**, and **review-required** / conflict files. Note: if Obsidian’s vault root is the Git repo root, prefer relative Markdown links inside `knowledge/` (see `governance/schema.md`); optionally open `knowledge/` as the vault root for bundle-absolute `/…` links.
