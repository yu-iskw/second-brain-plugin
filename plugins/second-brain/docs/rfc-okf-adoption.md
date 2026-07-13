# RFC: Adopt Open Knowledge Format (OKF) as the Canonical Knowledge Representation

**Status:** Adopted\
**Date:** 2026-07-13

## Decision

- OKF v0.1 is the canonical storage format for the knowledge bundle.
- Obsidian is an optional client/editor.
- Governance lives outside the OKF bundle under `governance/`.
- The repository remains Git-native and scriptless-first.
- Agent workflows maintain, verify, and repair the OKF bundle.

## Layout

```text
repository/
├── knowledge/          # OKF bundle root
│   ├── index.md        # may declare okf_version: "0.1"
│   ├── log.md
│   ├── concepts/
│   ├── entities/
│   ├── sources/
│   └── synthesis/
├── governance/         # outside OKF
│   ├── schema.md
│   ├── ontology.md
│   ├── policies.md
│   ├── quality-rubric.md
│   ├── source-ledger.md
│   ├── automation-state.md
│   ├── proposals/
│   └── reports/
├── raw/
├── output/
├── AGENTS.md
├── CLAUDE.md
├── .cursor/
└── .obsidian/          # optional
```

## Frontmatter

OKF core fields: `type` (open), `title`, `description`, `resource`, `tags`, `timestamp`.

Second Brain extensions: `knowledge_role`, `status`, `verification`, `confidence`, `sources`, `aliases`, `raw_path`, `created`, `updated`, `review_after`, `supersedes`, `contradicts`.

Unknown fields MUST be preserved on round-trip.

## Linking

Canonical documents use standard Markdown links, preferably bundle-absolute from `knowledge/`:

```md
[Orders](/entities/orders.md)
```

Wikilinks MAY be accepted during ingestion or legacy migration but SHALL NOT be emitted as canonical.

## Validation profiles

- **okf-core** — YAML frontmatter, non-empty `type`, reserved `index.md`/`log.md` structure, Markdown links, bundle layout.
- **second-brain-governed** — provenance, lifecycle enums, verification/confidence, contradictions, review policy, ledger/index/log consistency.

Profiles are enforced by curator/lint/verifier agents (scriptless). See `governance/schema.md`.

## Migration

1. Rename `wiki/` → `knowledge/`.
2. Move `meta/` → `governance/`.
3. Replace wikilinks with Markdown links.
4. Map closed `type` enum → `knowledge_role` + open OKF `type`.
5. Preserve unknown metadata.
6. Apply okf-core and second-brain-governed checks.
7. Keep Obsidian optional.

## Non-goals

Replace Obsidian; introduce a database; require MCP; require a vector DB; introduce mandatory runtime validator services.
