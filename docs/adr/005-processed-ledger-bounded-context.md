# ADR 005: Processed Ledger as Separate Bounded Context

## Status

Accepted

## Context

The processed ledger tracks which sources have been ingested. The proposal lifecycle tracks what happened operationally with each proposal. These answer fundamentally different questions:

- Processed ledger: "Did we already ingest this source?"
- Proposal lifecycle: "What happened with this proposal?"

Conflating them creates coupling: a proposal failure shouldn't affect the ledger's answer about other sources, and a ledger query shouldn't need to reconstruct proposal history.

## Decision

Two separate stores with distinct schemas, keys, and lifecycles.

### Processed Ledger

- Location: `.librarian/processed.json`
- Key: source path (not proposal id)
- States: `processed` | `skipped` | `errored`
- Written: only after successful apply completes entirely
- Contains: `operationId` for traceability

```json
{
  "entries": {
    "raw/articles/foo.md": {
      "status": "processed",
      "operationId": "op_01H...",
      "proposalId": "prop_abc123",
      "processedAt": "...",
      "hash": "sha256:..."
    }
  }
}
```

### Proposal Lifecycle

- Location: `.librarian/proposals/<id>/metadata.json`
- Key: proposal id
- States: `pending` → `applying` → `applied` | `failed` | `rolled_back`
- Written: throughout the entire lifecycle
- Contains: full transition history with operationId per attempt

### Coupling Point

The apply pipeline is the **only** place that writes to both stores. Order:

1. Write all wiki targets (verified)
2. Write proposal → `applied`
3. **Then and only then:** write processed ledger entry

The ledger never knows about proposals. The proposal store never knows about the ledger.

## Consequences

- Queries are simple: ledger lookup by path, proposal lookup by id
- Failure in one doesn't corrupt the other
- Can rebuild ledger from proposal history if needed
- Can rebuild proposal state from transaction records if needed
- Each context can evolve its schema independently

## References

- Sprint 2A plan: `docs/sprint-2a-plan.md` — Bounded Contexts section
- ADR 004: Transaction-like apply with operationId
