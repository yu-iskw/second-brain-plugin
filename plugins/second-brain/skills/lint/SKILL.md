---
name: lint
description: Produce a read-only health report for the second brain.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write
---

# Lint Second Brain

Delegate structural and epistemic analysis to `knowledge-curator`. Optionally ask `wiki-verifier` in `audit` mode to sanity-check the curator report against the live vault. Do not use mutation-mode verification for lint.

When `$ARGUMENTS` includes `incremental` (or the caller is `/second-brain:maintain`), request incremental curator scope; otherwise run a full audit.

Write only a timestamped report under `meta/reports/`. Do not modify wiki pages, ledgers, or governance files. For every finding include severity, evidence, affected files, safe-versus-review-required classification (per `meta/policies.md`), quality-rubric notes when relevant, and recommended action. Suggest `research-scout` for explicit gaps that need external candidates.
