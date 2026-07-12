---
name: synthesize
description: Create or refresh a cross-source synthesis page with explicit evidence, disagreement, and verification.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *)
---

# Synthesize Knowledge

Use `$ARGUMENTS` as the topic or proposal. Ask `knowledge-curator` to identify relevant canonical pages, evidence coverage, disagreements, and gaps. Create or update one bounded page under `wiki/synthesis/` through `knowledge-integrator`.

A synthesis page must distinguish evidence from interpretation, cite source and canonical pages, preserve conflicting views, state confidence and gaps, and avoid external facts not already ingested. Update the index and log, then require `wiki-verifier` to pass.

Do not use synthesis as a way to merge, delete, or silently supersede canonical pages.
