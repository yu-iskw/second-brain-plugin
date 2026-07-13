---
name: repair
description: Apply explicitly approved safe repairs from a second-brain lint report and verify the result.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *), Bash(git status *)
---

# Repair Second Brain

Read the report or findings supplied in `$ARGUMENTS`. Apply only approved repairs.

Safe automatic repairs are exactly those listed under Change control in `governance/policies.md`. Require explicit human approval for every review-required change class in that policy.

Delegate changes to `knowledge-integrator` with operation type `repair` and an approved change package derived from the lint findings (include the intended `knowledge/log.md` entry in that package). Require `wiki-verifier` (`mutation` mode) to pass on the full package. Do not mutate files after PASS. Retain unresolved findings in the report/summary.
