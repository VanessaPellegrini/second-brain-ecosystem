# Gaps & Tracking

This document tracks documented capabilities that do not yet exist in the implementation.

Last updated: 2026-05-13

## Sprint 2A — Reliability Core

| Gap | Description | Sprint 2A Section | Priority | Status |
|-----|-------------|-------------------|----------|--------|
| Proposal state model | No explicit state machine for proposals (pending/applying/applied/failed/rolled_back) | Section 1 | High | Not started |
| operationId correlation | No unique correlation ID per mutation attempt | Sections 1-2, 4 | High | Not started |
| Transaction-like apply | Apply is not atomic; partial applies leave wiki inconsistent | Section 2 | High | Not started |
| Apply rollback | No rollback mechanism on apply failure | Section 2 | High | Not started |
| Processed ledger separation | Ledger and proposal lifecycle are conflated | Bounded Contexts | High | Not started |
| Proposal inspection CLI | No `librarian proposal <id>` command | Section 3 | High | Not started |
| Proposal retry CLI | No `librarian proposal retry <id>` command | Section 3 | High | Not started |
| Proposal reset CLI | No `librarian proposal reset <id>` command | Section 3 | Medium | Not started |
| Index invalidation | No mechanism to detect stale index | Section 4 | High | Not started |
| Index rebuild command | No `librarian index rebuild` command | Section 4 | High | Not started |
| Index metadata | No `.librarian/index-metadata.json` with per-file tracking | Section 4 | High | Not started |
| `/orphans` correctness | Orphan detection may include proposals, temps, partials | Section 5 | Medium | Not started |
| `/orphans` graph-based | `/orphans` walks filesystem instead of using graph index | Section 5 | Medium | Not started |
| Contextual TUI alignment | TUI chat path diverges from CLI/harness context | Section 6 | Medium | Not started |
| Shared runtime context | CLI and TUI may duplicate logic instead of sharing | Section 6 | Medium | Not started |
| TUI proposal recovery UI | No UI for failed/stuck proposals | Section 3 | Medium | Not started |
| TUI index status display | No index status badge in TUI | Section 4 | Medium | Not started |

## Future (Sprint 2B+)

| Gap | Description | Priority | Status | Reason |
|-----|-------------|----------|--------|--------|
| Filesystem watchers | Real-time file change detection | Medium | Not started | Requires transactional base first |
| Autonomous loops | Background maintenance without trigger | Medium | Not started | Requires watchers + apply atomicity |
| Reconciliation engine | Detect and resolve wiki/raw conflicts | Medium | Not started | Requires watchers + index invalidation |
| Incremental indexing | Partial index updates | Medium | Not started | Requires rebuild + metadata model |
| Auto-apply | Automatic proposal application | Low | Not started | Requires full autonomy chain |

## Terminology Alignment

| Item | Status | Notes |
|------|--------|-------|
| Canonical vocabulary doc | Done | `docs/architecture/canonical-terms.md` |
| README privacy wording | Done | Root README.md and README.es.md |
| reviews/ vs .librarian/proposals/ | Done | Standard phrase applied in guides 04, 07, agent README |
| "AI maintenance" → "review-driven maintenance" | Done | All docs updated |
| Current Reality vs Future Direction | Done | Added to root READMEs |
| Landing page (DESIGN.md) wording | Pending | Needs alignment when implemented |

## References

- Sprint 2A plan: [`docs/sprint-2a-plan.md`](./sprint-2a-plan.md)
- Canonical vocabulary: [`docs/architecture/canonical-terms.md`](./architecture/canonical-terms.md)
- ADR 001: Review-driven pipeline
- ADR 002: Consent boundary inbox/raw
- ADR 003: Dual proposal surface
- ADR 004: Transaction-like apply with operationId
- ADR 005: Processed ledger as separate bounded context
- ADR 006: Index invalidation model
- Librarian repo: [github.com/Agents4Life/librarian](https://github.com/Agents4Life/librarian)
