# Source Ledger

| Source | Status | Source page | Last attempt | Notes |
|---|---|---|---|---|

Statuses: `new`, `analyzing`, `integrated`, `needs-review`, `rejected`, `superseded`, `failed`.

## Ownership

- `/second-brain:ingest` (or maintain’s ingest phase) sets `analyzing` before delegating to `source-analyst`.
- On early stop (insufficient provenance, ambiguous identity, prompt-injection risk), the ingest skill sets `needs-review` or `failed` and logs the reason.
- `knowledge-integrator` sets `integrated` (or `needs-review` / `failed`) as part of an `ingest` operation.
- Humans set `rejected` / `superseded`.
