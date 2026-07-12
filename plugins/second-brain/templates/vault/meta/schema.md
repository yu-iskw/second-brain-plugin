# Wiki Schema

## Directories

- `wiki/sources/`: one evidence-grounded page per ingested source
- `wiki/entities/`: people, organizations, products, places, and tools
- `wiki/concepts/`: ideas, methods, patterns, theories, and terms
- `wiki/synthesis/`: cross-source comparisons and analyses

## Required frontmatter

```yaml
---
type: source | entity | concept | synthesis
title: Human-readable title
aliases: []
status: draft | active | needs-review | deprecated
verification: unverified | partially-verified | verified | disputed
confidence: low | medium | high
sources: []
raw_path:
created: YYYY-MM-DD
updated: YYYY-MM-DD
review_after:
supersedes: []
contradicts: []
tags: []
---
```

`raw_path` is required when `type: source` and must point at the immutable file under `raw/**`. Leave `raw_path` empty for non-source pages. Dates use ISO 8601. Internal references use Obsidian `[[wikilinks]]`. A page title and aliases must not collide with an existing canonical page unless they identify the same subject with evidence.

Page lifecycle enums (`status`, `verification`, `confidence`) are defined only here; `AGENTS.md` references this schema.
