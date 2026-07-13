# Ontology

## Knowledge roles

Use `knowledge_role` for routing. OKF `type` remains an open descriptive string.

| knowledge_role | Directory | Default OKF `type` | Meaning |
| --- | --- | --- | --- |
| `source` | `knowledge/sources/` | `Source` | Faithful representation of one raw artifact |
| `entity` | `knowledge/entities/` | `Entity` | Person, organization, product, place, system, or tool (prefer specifics like `Person` when clear) |
| `concept` | `knowledge/concepts/` | `Concept` | Reusable idea, method, pattern, theory, term, or capability |
| `synthesis` | `knowledge/synthesis/` | `Synthesis` | Cross-source analysis distinguishing evidence from interpretation |

`second-brain-governed` requires `knowledge_role` to match the page’s directory (this table).

## Canonicalization rules

Prefer stable, human-readable singular titles. Use aliases for abbreviations and spelling variants. Do not combine entities solely because their names are similar. Do not create a new page when an existing page can accurately absorb the information. Record disputed identity or taxonomy in the page rather than guessing.
