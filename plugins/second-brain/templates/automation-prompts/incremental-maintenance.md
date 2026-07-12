# Incremental Second-Brain Maintenance

Maintain this Obsidian second-brain repository.

Follow `AGENTS.md` and all applicable Cursor rules. Run `/second-brain:maintain incremental`.

Constraints:

1. Never modify `raw/**`.
2. Process at most five new sources.
3. Do not delete, rename, merge, or split wiki pages.
4. Do not change schema, ontology, or policies.
5. Separate source analysis, integration, and verification.
6. Do not claim success unless the verifier passes.
7. Record contradictions and uncertainty rather than resolving them silently.
8. Update `wiki/log.md`, `meta/source-ledger.md`, and `meta/automation-state.md`.
9. Keep the change set within the risk budget in `AGENTS.md`.
10. Create a pull request summarizing evidence, changes, verification, and remaining review items.
