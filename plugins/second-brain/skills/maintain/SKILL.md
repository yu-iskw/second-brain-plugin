---
name: maintain
description: Run bounded, automation-safe second-brain maintenance across ingestion, linting, and safe repair.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *), Bash(git status *), Bash(git log *)
---

# Maintain Second Brain

This is the Cursor Automation entry point. Follow `AGENTS.md` and `meta/policies.md`.

1. Read `meta/automation-state.md` and repository status.
2. Refuse concurrent or dirty unrelated work.
3. Discover at most five new sources and run the ingest workflow.
4. Run an incremental lint over affected and linked pages.
5. Apply only unambiguous safe repairs.
6. Require independent verification after every mutation phase.
7. Update automation state, source ledger, and operation log.
8. Produce a PR-ready summary containing scope, sources, changed files, verification, unresolved review items, and risk-budget status.

Stop and request review when more than 20 wiki pages would change, more than 10 canonical pages would be created, governance files are touched, a high-impact contradiction is found, or destructive/semantic refactoring is indicated.
