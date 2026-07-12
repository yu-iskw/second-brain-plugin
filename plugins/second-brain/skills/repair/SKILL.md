---
name: repair
description: Apply explicitly approved safe repairs from a second-brain lint report and verify the result.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *), Bash(git status *)
---

# Repair Second Brain

Read the report or findings supplied in `$ARGUMENTS`. Apply only approved repairs.

Safe automatic repairs include adding a missing index entry, fixing a broken wikilink with exactly one unambiguous target, normalizing schema fields without changing meaning, adding a missing reciprocal link, and synchronizing ledgers.

Require explicit human approval for deletion, rename, merge, split, canonical identity changes, factual contradiction resolution, ontology changes, external facts, or semantic rewriting.

Delegate changes to `knowledge-integrator`, then require `wiki-verifier` to pass. Record the repair in `wiki/log.md` and retain unresolved findings.
