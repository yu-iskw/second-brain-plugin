# Ontology

## Knowledge roles

Use `knowledge_role` for routing. OKF `type` remains an open descriptive string.

- **Source** (`knowledge_role: source`): a faithful representation of one raw artifact. Default OKF `type`: `Source`.
- **Entity** (`knowledge_role: entity`): a uniquely identifiable person, organization, product, place, system, or tool. Default OKF `type`: `Entity` (more specific types such as `Person` or `Organization` are encouraged).
- **Concept** (`knowledge_role: concept`): a reusable idea, method, pattern, theory, term, or capability. Default OKF `type`: `Concept`.
- **Synthesis** (`knowledge_role: synthesis`): a cross-source analysis that distinguishes evidence from interpretation. Default OKF `type`: `Synthesis`.

## Canonicalization rules

Prefer stable, human-readable singular titles. Use aliases for abbreviations and spelling variants. Do not combine entities solely because their names are similar. Do not create a new page when an existing page can accurately absorb the information. Record disputed identity or taxonomy in the page rather than guessing. Preserve unknown frontmatter keys and tolerate unknown OKF `type` values.
