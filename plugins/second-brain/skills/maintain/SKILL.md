---
name: maintain
description: Run bounded, automation-safe second-brain maintenance across ingestion, linting, and safe repair.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *), Bash(git status *), Bash(git log *)
---

# Maintain Second Brain

Cursor Automation entry point. Follow `AGENTS.md` and `meta/policies.md`. Mode from `$ARGUMENTS`: `incremental` (default) or `full`. If `meta/automation-state.md` has an empty `last_successful_commit`, treat incremental lint/curator scope as `full` for this run (then record the commit).

1. Read `meta/automation-state.md` and repository status; refuse concurrent or dirty unrelated work when `write_run_active` is true.
2. Mark `write_run_active: true` via `knowledge-integrator` (`maintain-state`) before mutations.
3. Run the `/second-brain:ingest` workflow for at most five new/absent ledger sources.
4. Run `/second-brain:lint` with matching scope (`incremental` unless empty baseline forces `full`; `full` when requested).
5. Run `/second-brain:repair` only for unambiguous safe repairs listed in `meta/policies.md`.
6. Require `wiki-verifier` `PASS` after every mutation phase that changed wiki pages.
7. Always clear `write_run_active: false` via `maintain-state` on success, early stop, or failure; on success also update `last_successful_commit`, timestamps, ledgers, and operation log as applicable.
8. Produce a PR-ready summary: scope, sources, changed files, verification, unresolved review items, and risk-budget status from `AGENTS.md`.

Honor the automation risk budget in `AGENTS.md`; stop and request review when exceeded. Clearing `write_run_active` is mandatory even when stopping for review.
