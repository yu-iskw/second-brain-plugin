# Knowledge Schema (OKF + Second Brain)

The **OKF bundle** is `knowledge/`. Governance lives under `governance/` (outside the bundle). Ownership boundaries: `AGENTS.md`. Role semantics and default OKF `type` values: `governance/ontology.md`.

## Frontmatter

Every non-reserved `.md` under `knowledge/` MUST have parseable YAML frontmatter with a non-empty OKF `type`.

### OKF core

```yaml
---
type: Concept                 # REQUIRED open string
title: Human-readable title
description: One-line summary
resource:                     # optional URI
tags: []
timestamp: 2026-07-13T00:00:00Z
---
```

Consumers MUST tolerate unknown `type` values. Unknown frontmatter keys MUST be preserved on round-trip.

### Second Brain extensions

```yaml
knowledge_role: source | entity | concept | synthesis
status: draft | active | needs-review | deprecated
verification: unverified | partially-verified | verified | disputed
confidence: low | medium | high
sources: []
aliases: []
raw_path:                     # required when knowledge_role: source → raw/**
created: YYYY-MM-DD
updated: YYYY-MM-DD
review_after:
supersedes: []
contradicts: []
```

Set `timestamp` from `updated` (or current UTC) on meaningful writes. Title/alias collisions require evidence of the same subject. Lifecycle enums are defined only here.

## Linking

Canonical links are standard Markdown; prefer bundle-absolute paths from `knowledge/`:

```md
[Orders](/entities/orders.md)
```

Relative links are allowed.

**Wikilink severity**

- Emitting new `[[wikilinks]]` fails **okf-core**.
- Pre-existing wikilinks are warnings (curator / safe repair); ingest and setup MAY convert unambiguous ones to Markdown.
- Broken links: soft under okf-core; **second-brain-governed** requires newly introduced Markdown links to resolve (or be flagged for review).

## Reserved files

- `index.md`: no frontmatter except optional `okf_version: "0.1"` on the bundle-root index. Body: section headings + bullet links with short descriptions.
- `log.md`: date headings `YYYY-MM-DD` (newest first) and/or operation entries; not a concept document.

## Validation profiles

Label schema-related lint findings with the profile id.

### okf-core

1. Every non-reserved `knowledge/**/*.md` has parseable YAML frontmatter with non-empty `type`.
2. Reserved `index.md` / `log.md` follow the structures above when present.
3. Bundle root is `knowledge/`.
4. Do not emit new wikilinks (see Linking).
5. Do not fail solely for missing optional fields, unknown `type`/keys, or pre-existing broken links.

### second-brain-governed

1. `knowledge_role` present and consistent with directory placement (see ontology).
2. Lifecycle enums valid; `raw_path` set for sources.
3. Provenance: material claims cite sources; contradictions/supersedes stay explicit.
4. Review policy and safe-repair whitelist: `governance/policies.md`.
5. Index, log, and ledger/automation-state agree with the change package.
6. Newly introduced Markdown links resolve (or are explicitly flagged for review).
