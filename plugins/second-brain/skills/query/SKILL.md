---
name: query
description: Answer questions from the maintained OKF knowledge bundle with explicit provenance and uncertainty.
allowed-tools: Read, Glob, Grep
---

# Query Second Brain

Answer `$ARGUMENTS` from the knowledge bundle, not from unsupported model memory.

1. Start with `knowledge/index.md` and relevant metadata.
2. Search canonical pages and follow useful Markdown links (per `governance/schema.md`).
3. Consult source pages for claim-level support; read `raw/` only as a last resort.
4. Separate sourced statements, synthesis, inference, disagreement, and unknowns.
5. Cite knowledge pages with Markdown links per `governance/schema.md`.

Do not mutate the repository. When the answer creates durable new synthesis, recommend `/second-brain:synthesize` rather than writing opportunistically.
