---
name: synthesize
description: Create or refresh a cross-source synthesis page with explicit evidence, disagreement, and verification.
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash(git diff *), Bash(git status *)
---

# Synthesize Knowledge

Use `$ARGUMENTS` as the topic or proposal. Ask `knowledge-curator` with scope `topic`, passing the topic string plus seed pages from `knowledge/index.md` and search hits. For caller-approved external gap research, delegate candidates to `research-scout` without ingesting them. Create or update one bounded page under `knowledge/synthesis/` through `knowledge-integrator` with operation type `synthesize`.

Follow the integrator `synthesize` contract and `AGENTS.md` invariants. Update the index and log, then require `wiki-verifier` (`mutation` mode) to pass.
