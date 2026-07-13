# RFC: Adopt Open Knowledge Format (OKF) as the Canonical Knowledge Representation

**Status:** Adopted\
**Date:** 2026-07-13

## Decision

- OKF v0.1 is the canonical storage format for the knowledge bundle (`knowledge/`).
- Obsidian is an optional client/editor.
- Governance lives outside the OKF bundle under `governance/`.
- The repository remains Git-native and scriptless-first.
- Agent workflows maintain, verify, and repair the OKF bundle.

## Normative detail

Materialized after `/second-brain:setup`:

- Format, linking, and profiles: `governance/schema.md`
- Roles: `governance/ontology.md`
- Safe repairs and concurrency: `governance/policies.md`
- Agent contract: `AGENTS.md`

## Migration

Legacy `wiki/` + `meta/` layouts: follow `/second-brain:setup` (rename, link rewrite, frontmatter map, conflict reporting).

## Non-goals

Replace Obsidian; introduce a database; require MCP; require a vector DB; introduce mandatory runtime validator services.

## Upstream

https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
