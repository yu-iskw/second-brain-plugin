---
name: setup
description: Initialize or upgrade a Git-native OKF second-brain repository for governed knowledge maintenance.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git mv wiki knowledge), Bash(git mv meta governance), Bash(mv wiki knowledge), Bash(mv meta governance), Bash(mkdir *)
---

# Setup Second Brain

Initialize or upgrade the current directory as a governed OKF knowledge repository. Obsidian is optional. Shell renames are limited to `wiki`→`knowledge` and `meta`→`governance` only.

Templates live under `${CLAUDE_PLUGIN_ROOT}/templates/vault/`. Creating a missing empty `raw/**/.gitkeep` is allowed; never overwrite or edit source files under `raw/`.

## Ordered state machine (run top to bottom; one action per matching row)

Evaluate `governance/{schema,ontology,policies,quality-rubric}.md` and `AGENTS.md` **per file** (independent decisions; never batch-replace sibling governance files).

| Condition | Action |
| --- | --- |
| `wiki/` exists and `knowledge/` does not | `git mv`/`mv` `wiki` → `knowledge` |
| `wiki/` and `knowledge/` both exist | Conflict: do not merge; list review-required |
| `meta/` exists and `governance/` does not | `git mv`/`mv` `meta` → `governance` |
| `meta/` and `governance/` both exist | Conflict: do not merge; list review-required |
| Any of `governance/{schema,ontology,policies,quality-rubric}.md` or `AGENTS.md` is **missing** or **pre-OKF** | For **each** file independently: if missing or pre-OKF, backup existing content to `governance/proposals/legacy-<name>-backup.md` when present, then materialize the OKF template for **that file only**. **Pre-OKF `schema.md`:** no `okf-core`, mandates `[[wikilinks]]` as canonical, or closed `type:` enum without `knowledge_role`. **Pre-OKF other governance files:** references `wiki/**` or `meta/**` instead of `knowledge/**` / `governance/**`. **Pre-OKF `AGENTS.md`:** describes `wiki/**`/`meta/**` or lacks OKF ownership boundaries. **Skip** files already OKF-conformant (next row). Mark review-required for any backup-then-replace. |
| OKF-conformant governance file exists and differs from template in substance | Preserve user file unchanged; write template as `governance/proposals/<name>.okf-template.md`; list under **preserved** / conflict |
| Required OKF files/dirs still missing after the above | Materialize missing templates only (including `.gitkeep` dirs under `knowledge/{sources,entities,concepts,synthesis}`, `governance/{proposals,reports}`, `raw/assets`, `output`) |
| Pages under `knowledge/` still have `[[` or legacy closed `type:` | Grep first; edit matching files only; cap at 20 pages per run (same risk budget as `AGENTS.md`); leave remainder as review-required |

**Do not materialize empty `knowledge/` or `governance/` trees before the rename rows.** Renames and per-file governance upgrades must run before filling gaps from templates.

After governance is OKF-conformant, rewrite Grep hits: unambiguous wikilinks → Markdown (relative links under `knowledge/`); map legacy closed `type` → `knowledge_role` + open OKF `type` per schema/ontology; preserve unknown keys; set `timestamp` from `updated` when present.

## Required end state

- `AGENTS.md`, `CLAUDE.md` (imports `AGENTS.md`)
- `governance/{schema,ontology,policies,quality-rubric,source-ledger,automation-state}.md`
- `knowledge/index.md` (optional `okf_version: "0.1"`), `knowledge/log.md`
- `.cursor/rules/*.mdc`
- directory `.gitkeep` placeholders as in the template tree

Finish with a manifest of **created**, **migrated**, **preserved**, and **review-required** / conflict files. Linking rules: `governance/schema.md`.
