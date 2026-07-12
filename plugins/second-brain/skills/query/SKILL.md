---
name: query
description: Answer questions from the maintained wiki with explicit provenance and uncertainty.
allowed-tools: Read, Glob, Grep
---

# Query Second Brain

Answer `$ARGUMENTS` from the wiki, not from unsupported model memory.

1. Start with `wiki/index.md` and relevant metadata.
2. Search canonical pages and follow useful wikilinks.
3. Consult source pages for claim-level support; read `raw/` only as a last resort.
4. Separate sourced statements, synthesis, inference, disagreement, and unknowns.
5. Cite vault pages with `[[wikilinks]]`.

Do not mutate the vault. When the answer creates durable new synthesis, recommend `/second-brain:synthesize` rather than writing opportunistically.
