# Knowledge Schema (OKF + Second Brain)

The **OKF bundle** is `knowledge/`. Governance lives under `governance/` (outside the bundle). Ownership boundaries: `AGENTS.md`. Role semantics and directory placement: `governance/ontology.md`.

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

Canonical links are standard Markdown. **Default: relative links within `knowledge/`** (works when the Git repo root is also an Obsidian vault root).

```md
[Orders](../entities/orders.md)
```

Bundle-absolute `/entities/orders.md` is optional when the OKF bundle directory itself is the consumption root (for example Obsidian vault root = `knowledge/`).

### Wikilink severity

- Emitting new `[[wikilinks]]` fails **okf-core**.
- Pre-existing wikilinks are warnings (curator / setup / repair); do not convert on ordinary ingest.
- Broken links: soft under okf-core; **second-brain-governed** requires newly introduced Markdown links to resolve (or be flagged for review).

## Reserved files

- `index.md`: no frontmatter except optional `okf_version: "0.1"` on the bundle-root index. Body: section headings + bullet links with short descriptions.
- `log.md`: date headings `YYYY-MM-DD` (newest first) and/or operation entries; not a concept document.

## Validation profiles

Label schema-related lint findings with the profile id. In **mutation** verify, apply profiles to **touched non-reserved** knowledge pages in the diff. For newly added Markdown links, only require that targets **resolve** (or be flagged)—do not run full profiles on one-hop neighbors. Reserved `index.md` / `log.md` are checked only under okf-core reserved-file rules, never under second-brain-governed field requirements.

### okf-core

1. Every checked non-reserved `knowledge/**/*.md` has parseable YAML frontmatter with non-empty `type`.
2. Reserved `index.md` / `log.md` follow the structures above when present.
3. Bundle root is `knowledge/`.
4. Do not emit new wikilinks (see Linking).
5. Do not fail solely for missing optional fields, unknown `type`/keys, or pre-existing broken links.

### second-brain-governed

Applies to non-reserved knowledge pages only (not `index.md` / `log.md`).

1. `knowledge_role` present and consistent with directory placement (`governance/ontology.md`).
2. Lifecycle enums valid; `raw_path` set for sources.
3. Provenance: material claims cite sources; contradictions/supersedes stay explicit.
4. Review policy and safe-repair whitelist: `governance/policies.md`.
5. Newly introduced Markdown links resolve (or are explicitly flagged for review).
