---
name: lint
description: Produce a read-only health report for the second brain.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Bash(git diff *), Bash(git log *), Bash(git rev-parse *)
---

# Lint Second Brain

Delegate structural and epistemic analysis to `knowledge-curator`.

Scope:

- `full` when `$ARGUMENTS` includes `full`, when `last_successful_commit` is empty, or when maintain forces full.
- `incremental` when `$ARGUMENTS` includes `incremental` or the caller is maintain in incremental mode with a non-empty baseline: compute the changed-page list via `git diff --name-only <last_successful_commit>` (plus one-hop links you discover), and pass that list to the curator.
- Prefer `incremental` for routine maintain; prefer `full` for an explicit `/second-brain:lint` without args.

When `$ARGUMENTS` includes `verify` or `strict`, also ask `wiki-verifier` in `audit` mode to sanity-check the curator report. Otherwise do not invoke the verifier.

Write only a timestamped report under `meta/reports/`. Do not modify wiki pages, ledgers, or governance files. For every finding include severity, evidence, affected files, safe-versus-review-required classification (per `meta/policies.md`), quality-rubric notes when relevant, and recommended action. Suggest `research-scout` for explicit gaps that need external candidates.
