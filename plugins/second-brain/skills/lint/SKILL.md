---
name: lint
description: Produce a read-only health report for the second brain.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write
---

# Lint Second Brain

Delegate structural and epistemic analysis to `knowledge-curator`.

Scope: use `incremental` when `$ARGUMENTS` includes `incremental` or the caller is maintain in incremental mode; use `full` when `$ARGUMENTS` includes `full`, when maintain forces full because `last_successful_commit` is empty, or when no incremental hint is present. Prefer `incremental` for routine maintain; prefer `full` for an explicit `/second-brain:lint` without args.

When `$ARGUMENTS` includes `verify` or `strict`, also ask `wiki-verifier` in `audit` mode to sanity-check the curator report. Otherwise do not invoke the verifier.

Write only a timestamped report under `meta/reports/`. Do not modify wiki pages, ledgers, or governance files. For every finding include severity, evidence, affected files, safe-versus-review-required classification (per `meta/policies.md`), quality-rubric notes when relevant, and recommended action. Suggest `research-scout` for explicit gaps that need external candidates.
