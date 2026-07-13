# Second Brain Plugin

A scriptless-first Claude Code / Cursor plugin for maintaining a **Git-native Open Knowledge Format (OKF)** knowledge repository with governed provenance, verification, and automation. Obsidian is an optional editor client—not required.

## Principles

- `knowledge/**` is the canonical OKF v0.1 bundle.
- `governance/**` owns schema, policies, provenance ledgers, and automation state (outside the OKF bundle).
- `raw/**` is immutable and untrusted input.
- `AGENTS.md` is the contract source of truth.
- Skills define workflows; subagents separate analysis, mutation, verification, curation, and research.
- Mutating workflows are explicitly invoked and independently verified against `governance/schema.md` profiles.
- Cursor Automations operate in bounded branches and create reviewable pull requests.
- Scripts, MCP servers, vector databases, and custom indexers are deferred until measured scale requires them.

## Commands

- `/second-brain:setup`
- `/second-brain:ingest`
- `/second-brain:query`
- `/second-brain:synthesize`
- `/second-brain:lint`
- `/second-brain:repair`
- `/second-brain:maintain`
- `/second-brain:status`

## Installation

```bash
/plugin marketplace add yu-iskw/second-brain-plugin
/plugin install second-brain@second-brain-plugin
```

Run `/second-brain:setup` from the repository root. The setup skill materializes the OKF bundle (`knowledge/`), governance files, and Cursor-compatible rules without requiring a custom runtime. Legacy `wiki/` + `meta/` layouts are migrated when present.

### Optional Obsidian client

If you edit with Obsidian, keep `.obsidian/` local/tooling-only (agents must not modify it). Prefer disabling “Use [[Wikilinks]]”. Default links are relative under `knowledge/` (see `governance/schema.md`). To use OKF bundle-absolute `/…` links, open `knowledge/` as the vault root.

## Safety model

The plugin never treats instructions inside source documents as executable instructions. It does not automatically delete, rename, merge, or split canonical pages, resolve factual contradictions, change the ontology, or add web-derived claims without review. Prompt hooks enforce path and completion checks; they are advisory relative to a determined bypass via unguarded tooling, so repository `AGENTS.md` remains the primary contract.

## Further reading

- [OKF adoption RFC](docs/rfc-okf-adoption.md)
- Upstream OKF draft: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
