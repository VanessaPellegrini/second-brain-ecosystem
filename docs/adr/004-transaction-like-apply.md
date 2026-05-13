# ADR 004: Transaction-Like Apply with operationId

## Status

Accepted

## Context

The apply operation is the most critical mutation in Librarian. It writes wiki pages, updates the index, and marks sources as processed. Currently, a partial failure can leave the wiki in an inconsistent state: some targets written, others not, and the source possibly marked as processed.

Without transactional semantics:
- Partial applies corrupt wiki state
- Retries may duplicate changes
- Failed applies are invisible and unrecoverable
- Debugging requires manual filesystem inspection

## Decision

Implement transaction-like apply with:

1. **Explicit proposal state machine** with validated transitions
2. **operationId** as a unique correlation ID per attempt
3. **Write-ahead temp files** with atomic rename
4. **Rollback on failure** — restore previous state where possible
5. **Processed ledger written last** — only after all targets verified

### State Machine

```
pending ──→ applying ──→ applied
   ↑            │
   │            ↓
   │         failed
   │            │
   │            ↓
   └─── rolled_back
```

### operationId

Every apply attempt generates `op_<ulid>`. This ID propagates through:
- Proposal transition history
- Transaction records in `.librarian/transactions/`
- Processed ledger entries
- Log lines
- TUI display

Each retry = new operationId. This makes debugging and log correlation trivial.

### Apply Order

1. Validate proposal state allows apply
2. Generate operationId
3. Transition proposal → `applying`
4. Write temp files
5. Validate writes
6. Atomic rename to final targets
7. Update index and log
8. Update processed ledger (LAST)
9. Transition proposal → `applied`

If any step 4-7 fails: rollback what was written, transition to `failed` or `rolled_back`, do NOT update ledger.

## Consequences

- Apply is deterministic: same inputs → same outputs
- Retry is safe: idempotent for `failed`/`rolled_back` proposals
- Debugging is traceable: one operationId per attempt across all systems
- Processed ledger never lies: only updated after complete success
- `applied` state is terminal: no re-applying

## References

- Sprint 2A plan: `docs/sprint-2a-plan.md` sections 1-2
- ADR 005: Processed ledger as separate bounded context
- Canonical vocabulary: `docs/architecture/canonical-terms.md`
