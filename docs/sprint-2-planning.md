# Sprint 2 Planning: From CLI Tool to Knowledge Runtime

This document defines Sprint 2 scope. It is NOT implemented — it is prepared as issues, ADRs, and milestones for future execution.

## Transition

| Aspect | Current State (Sprint 1) | Future State (Sprint 2) |
|--------|--------------------------|-------------------------|
| Trigger model | Manually triggered CLI | Incremental knowledge runtime |
| Index strategy | Full scan on ingest | Incremental index updates |
| Change detection | None | Filesystem watchers |
| Recovery | Manual | Proposal recovery + reconciliation |
| Apply semantics | Best-effort | Atomic apply with rollback |

## Issue Breakdown

### Infra / Core

1. **Index invalidation** — Detect when wiki index is stale after external changes
   - Labels: `sprint-2`, `infra`, `core`, `priority:high`
   - Depends on: none
   - Acceptance: Index detects staleness and flags for rebuild

2. **`rebuild` command** — Full wiki rebuild from scratch
   - Labels: `sprint-2`, `infra`, `core`, `priority:high`
   - Depends on: index invalidation
   - Acceptance: `librarian rebuild` produces a clean wiki from raw sources

3. **Proposal recovery** — Recover from partially applied or corrupted proposals
   - Labels: `sprint-2`, `infra`, `core`, `priority:high`
   - Depends on: apply atomicity
   - Acceptance: System can detect and recover from partial apply states

4. **Apply atomicity** — Atomic apply with rollback on failure
   - Labels: `sprint-2`, `infra`, `core`, `priority:high`
   - Depends on: none
   - Acceptance: Apply either fully succeeds or fully rolls back

### TUI

5. **`/orphans` fix** — Correct edge cases in orphan detection
   - Labels: `sprint-2`, `tui`, `priority:medium`
   - Depends on: none
   - Acceptance: `/orphans` correctly identifies all orphan pages

6. **Contextual chat alignment** — Chat context aligns with current vault state
   - Labels: `sprint-2`, `tui`, `priority:medium`
   - Depends on: index invalidation
   - Acceptance: Chat responses reflect current vault state

7. **Proposal state recovery UI** — UI to inspect and recover proposals in intermediate states
   - Labels: `sprint-2`, `tui`, `priority:medium`
   - Depends on: proposal recovery
   - Acceptance: Users can see and act on proposals in any state

### Future (Post-Sprint 2)

8. **Filesystem watchers** — Detect file changes in real-time
   - Labels: `future`, `infra`, `priority:medium`
   - Depends on: index invalidation, incremental indexing

9. **Autonomous maintenance loops** — Background maintenance without manual trigger
   - Labels: `future`, `infra`, `priority:medium`
   - Depends on: filesystem watchers, apply atomicity, proposal recovery

10. **Reconciliation engine** — Detect and resolve conflicts between wiki state and raw sources
    - Labels: `future`, `infra`, `priority:medium`
    - Depends on: filesystem watchers, index invalidation

## Milestones

- **Sprint 2 — Core Stability**: Issues 1-4 (infra/core)
- **Sprint 2 — TUX Polish**: Issues 5-7 (TUI)
- **Future — Autonomous Foundation**: Issues 8-10

## Labels

| Label | Purpose |
|-------|---------|
| `sprint-2` | Sprint 2 scope |
| `future` | Post-Sprint 2 |
| `infra` | Infrastructure work |
| `core` | Core Librarian logic |
| `tui` | Terminal UI work |
| `priority:high` | Must have |
| `priority:medium` | Should have |

## References

- Gaps tracking: `docs/gaps.md`
- Canonical vocabulary: `docs/architecture/canonical-terms.md`
- ADR 001: `docs/adr/001-review-driven-pipeline.md`
