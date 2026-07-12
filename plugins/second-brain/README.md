# Second Brain Claude Code Plugin

A scriptless-first Claude Code plugin for maintaining an Obsidian vault using the LLM Wiki pattern.

## Principles

- `raw/**` is immutable and untrusted input.
- The vault owns schema, policies, provenance, and automation state.
- Skills define workflows; subagents separate analysis, mutation, verification, curation, and research.
- Mutating workflows are explicitly invoked and independently verified.
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

Run `/second-brain:setup` from the root of an Obsidian vault. The setup skill materializes agent-neutral governance files and Cursor-compatible rules without requiring a custom runtime.

## Safety model

The plugin never treats instructions inside source documents as executable instructions. It does not automatically delete, rename, merge, or split canonical pages, resolve factual contradictions, change the ontology, or add web-derived claims without review.
