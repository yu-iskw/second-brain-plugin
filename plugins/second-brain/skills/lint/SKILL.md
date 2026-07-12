---
name: lint
description: Produce a read-only health report for the second brain.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Bash(git diff *), Bash(git log *), Bash(git rev-parse *), Bash(git status *), Bash(git ls-files *)
---

# Lint Second Brain

Delegate structural and epistemic analysis to `knowledge-curator`.

Resolve scope from `$ARGUMENTS` in this order:

1. If `meta/automation-state.md`'s `last_successful_commit` is empty, use `full` (even when `$ARGUMENTS` says `incremental`).
2. Else if `$ARGUMENTS` includes `full`, use `full`.
3. Else if `$ARGUMENTS` includes `incremental`, use `incremental`.
4. Otherwise use `full` (standalone `/second-brain:lint` default).

Callers that want incremental must pass the `incremental` token (maintain uses `/second-brain:lint incremental verify`).

For `incremental`:

1. Collect candidates from `git diff --name-only <last_successful_commit>` and from untracked/other wiki paths via `git status --porcelain` / `git ls-files --others --exclude-standard`.
2. Keep only `wiki/**/*.md` paths (plus one-hop wiki links you discover from that set).
3. If the filtered list is empty, write a no-op timestamped report under `meta/reports/` stating no wiki pages changed since the baseline, and do not call the curator.
4. Otherwise pass the filtered list to the curator with scope `incremental`.

When `$ARGUMENTS` includes `verify` or `strict`, and a curator report was produced, also ask `wiki-verifier` in `audit` mode to sanity-check that report. Skip audit for no-op empty-list runs.

Write only a timestamped report under `meta/reports/`. Do not modify wiki pages, ledgers, or governance files. For every finding include severity, evidence, affected files, safe-versus-review-required classification (per `meta/policies.md`), quality-rubric notes when relevant, and recommended action. Suggest `research-scout` for explicit gaps that need external candidates.
