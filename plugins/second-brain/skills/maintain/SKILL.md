---
name: maintain
description: Run bounded, automation-safe second-brain maintenance across ingestion, linting, and safe repair.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *), Bash(git status *), Bash(git log *)
---

# Maintain Second Brain

Cursor Automation entry point. Follow `AGENTS.md` and `meta/policies.md`. Mode from `$ARGUMENTS`: `incremental` (default) or `full`. If `meta/automation-state.md` has an empty `last_successful_commit`, treat incremental lint/curator scope as `full` for this run (then record the commit).

1. Read `meta/automation-state.md` and repository status. If `write_run_active` is true, check whether another write run is actually in progress; if not, `force-unlock` via `maintain-state` (log the reason) before continuing. Independently refuse when the worktree has dirty unrelated changes outside the expected automation branch/scope.
2. Mark `write_run_active: true` via `knowledge-integrator` (`maintain-state`) before mutations.
3. Run the `/second-brain:ingest` workflow for at most five new/absent ledger sources.
4. Run `/second-brain:lint verify` with matching scope (`incremental` unless empty baseline forces `full`; `full` when requested). For incremental, ensure lint computes a wiki-filtered changed-page list for the curator.
5. Run `/second-brain:repair` only for unambiguous safe repairs listed in `meta/policies.md` (and confirmed safe by lint’s verified report).
6. Require `wiki-verifier` `PASS` after every **content** mutation phase (ingest integration, repair, synthesize). Log/ledger-only early stops use verification `N/A` and do not need mutation PASS.
7. Always clear `write_run_active: false` via `maintain-state` on success, early stop, or failure; on success also update `last_successful_commit`, timestamps, ledgers, and operation log as applicable. Optionally run a final maintain-completion verify that checks the cleared flag.
8. Produce a PR-ready summary: scope, sources, changed files, verification, unresolved review items, and risk-budget status from `AGENTS.md`.

Honor the automation risk budget in `AGENTS.md`; stop and request review when exceeded. Clearing `write_run_active` is mandatory even when stopping for review.
