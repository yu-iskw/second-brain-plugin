---
name: lint
description: Produce a read-only health report for the second brain.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write
---

# Lint Second Brain

Delegate structural and epistemic analysis to `knowledge-curator`, then independent consistency checking to `wiki-verifier`.

Check broken and ambiguous wikilinks, orphan pages, duplicate concepts, missing provenance, schema drift, stale claims, unresolved contradictions, index and ledger inconsistencies, weak cross-references, and missing synthesis.

Write a timestamped report under `meta/reports/`. Do not modify wiki pages. For every finding include severity, evidence, affected files, safe-versus-review-required classification, and recommended action.
