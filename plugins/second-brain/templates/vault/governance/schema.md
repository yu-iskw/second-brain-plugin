# Knowledge Schema (OKF + Second Brain)

The repository root is a Git-native knowledge platform. The **OKF bundle** is the `knowledge/` directory. Governance artifacts live under `governance/` and are outside the OKF bundle.

## Directories

OKF bundle (`knowledge/`):

- `knowledge/sources/`: one evidence-grounded page per ingested source
- `knowledge/entities/`: people, organizations, products, places, and tools
- `knowledge/concepts/`: ideas, methods, patterns, theories, and terms
- `knowledge/synthesis/`: cross-source comparisons and analyses
- `knowledge/index.md`: progressive-disclosure index (optional root frontmatter: `okf_version` only)
- `knowledge/log.md`: chronological operation history

Governance (outside OKF):

- `governance/schema.md`, `ontology.md`, `policies.md`, `quality-rubric.md`
- `governance/source-ledger.md`, `automation-state.md`
- `governance/proposals/`, `governance/reports/`

## Frontmatter

Every non-reserved `.md` file under `knowledge/` MUST have parseable YAML frontmatter with a non-empty OKF `type`.

### OKF core (canonical)

```yaml
---
type: Concept                 # REQUIRED open string (not a closed enum)
title: Human-readable title
description: One-line summary
resource:                     # optional URI for an underlying asset
tags: []
timestamp: 2026-07-13T00:00:00Z
---
```

Default `type` values when none better fits: `Source`, `Entity`, `Concept`, `Synthesis`. Consumers MUST tolerate unknown types.

### Second Brain extensions

```yaml
knowledge_role: source | entity | concept | synthesis
status: draft | active | needs-review | deprecated
verification: unverified | partially-verified | verified | disputed
confidence: low | medium | high
sources: []
aliases: []
raw_path:
created: YYYY-MM-DD
updated: YYYY-MM-DD
review_after:
supersedes: []
contradicts: []
```

- `knowledge_role` routes pages into the directories above and replaces the former closed `type` enum.
- `raw_path` is required when `knowledge_role: source` and must point at the immutable file under `raw/**`. Leave empty for non-source pages.
- Set OKF `timestamp` from `updated` (or current UTC) on meaningful writes.
- Dates use ISO 8601.
- Unknown frontmatter keys MUST be preserved on round-trip.
- A page title and aliases must not collide with an existing canonical page unless they identify the same subject with evidence.

Page lifecycle enums (`status`, `verification`, `confidence`) are defined only here; `AGENTS.md` references this schema.

## Linking

Canonical internal references use standard Markdown links. Prefer bundle-absolute paths from the `knowledge/` root:

```md
[Orders](/entities/orders.md)
```

Relative links (`./other.md`) are allowed. Wikilinks (`[[...]]`) MAY be accepted during ingest or legacy migration but SHALL NOT be emitted as canonical. Broken links are soft failures under okf-core (warn); second-brain-governed may require resolution for newly introduced links.

## Reserved files

- `index.md`: no frontmatter except optional `okf_version: "0.1"` on the bundle-root index. Body uses section headings and bullet links with short descriptions.
- `log.md`: date headings `YYYY-MM-DD` (newest first) or operation entries; not a concept document.

## Validation profiles

### okf-core

Enforce on every knowledge document / bundle check:

1. Every non-reserved `.md` under `knowledge/` has parseable YAML frontmatter.
2. Every frontmatter has non-empty `type`.
3. Reserved `index.md` / `log.md` follow the structures above when present.
4. Bundle layout uses `knowledge/` as the OKF root.
5. Canonical links are Markdown (not wikilinks).

Do not fail solely for missing optional fields, unknown `type` values, unknown extra keys, or pre-existing broken links.

### second-brain-governed

Adds (for mutation and governed audit):

1. `knowledge_role` present and consistent with directory placement.
2. Lifecycle enums valid (`status`, `verification`, `confidence`).
3. Provenance: material claims cite sources; `raw_path` set for sources.
4. Contradictions/supersedes remain explicit; no silent winner.
5. Review policy and safe-repair whitelist per `governance/policies.md`.
6. Index, log, and ledger/automation-state agree with the change package.
7. Newly introduced Markdown links resolve (or are explicitly flagged for review).

Lint findings SHOULD label the profile id (`okf-core` or `second-brain-governed`).
