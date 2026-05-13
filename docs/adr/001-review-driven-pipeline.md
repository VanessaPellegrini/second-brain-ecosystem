# ADR 001: Review-Driven Knowledge Maintenance Pipeline

## Status

Accepted

## Context

Librarian needs a clear architectural identity. The system currently operates as a manually triggered, proposal-based CLI tool. There is a temptation to describe it as "autonomous" or "self-maintaining" in documentation, but those capabilities do not exist yet.

## Decision

We describe Librarian as a **review-driven knowledge maintenance pipeline**. This is the canonical description until autonomous capabilities (watchers, loops, reconciliation) are actually implemented.

The core workflow is:

1. User triggers an operation (ingest, query, lint)
2. Librarian generates a proposal in `.librarian/proposals/`
3. Proposal surfaces in `reviews/` as human-readable export
4. User reviews and approves via CLI
5. Approved proposal is applied to the wiki

All mutations go through this cycle. No direct wiki writes without approval.

## Consequences

- Documentation accurately reflects current capabilities
- Users and contributors are not confused by overpromises
- The architecture is honest about its current state
- Future autonomous features can be added incrementally without breaking the review-driven foundation
- The review-driven model remains useful even after automation (as a safety net)

## References

- Canonical vocabulary: `docs/architecture/canonical-terms.md`
