---
name: lint
description: Produce a read-only health report for the OKF second-brain knowledge bundle.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Bash(git diff *), Bash(git log *), Bash(git rev-parse *), Bash(git status *), Bash(git ls-files *)
---

# Lint Second Brain

Delegate structural and epistemic analysis to `knowledge-curator`.

Resolve scope from `$ARGUMENTS` in this order:

1. If `governance/automation-state.md`'s `last_successful_commit` is empty, use `full` (even when `$ARGUMENTS` says `incremental`).
2. Else if `$ARGUMENTS` includes `full`, use `full`.
3. Else if `$ARGUMENTS` includes `incremental`, use `incremental`.
4. Otherwise use `full` (standalone `/second-brain:lint` default).

Callers that want incremental must pass the `incremental` token (maintain uses `/second-brain:lint incremental verify`).

For `incremental`:

1. Collect candidates from `git diff --name-only <last_successful_commit>` and from untracked/other knowledge paths via `git status --porcelain` / `git ls-files --others --exclude-standard`.
2. Keep only `knowledge/**/*.md` paths (plus one-hop knowledge Markdown links you discover from that set).
3. If the filtered list is empty, write a no-op timestamped report under `governance/reports/` stating no knowledge pages changed since the baseline, and do not call the curator.
4. Otherwise pass the filtered list to the curator with scope `incremental`.

When `$ARGUMENTS` includes `verify` or `strict`, and a curator report was produced, also ask `wiki-verifier` in `audit` mode to sanity-check that report. Skip audit for no-op empty-list runs.

Write only a timestamped report under `governance/reports/`. Do not modify knowledge pages, ledgers, or governance policy files. For every finding include:

- severity
- **profile** id: `okf-core` or `second-brain-governed`
- evidence
- affected files
- safe-versus-review-required classification (per `governance/policies.md`)
- quality-rubric notes when relevant
- recommended action

Suggest `research-scout` for explicit gaps that need external candidates.
