# ADR 003: Dual Surface for Proposals (reviews/ + .librarian/proposals/)

## Status

Accepted

## Context

Proposals need two representations: a machine-readable source of truth for the system, and a human-readable surface for review. Combining them creates friction for either humans or machines.

## Decision

Two separate locations with distinct roles:

- `reviews/` is a human-readable review and export surface.
- `.librarian/proposals/` is the internal proposal source of truth.

The standard phrase used in all documentation:

> `reviews/` is a human-readable review and export surface. `.librarian/proposals/` is the internal proposal source of truth.

This exact phrase must appear consistently in: README, guides, architecture docs, PRD, and any future website.

## Consequences

- Clear separation of concerns
- Consistent wording across all documentation
- Users understand that `reviews/` is for them, `.librarian/proposals/` is for the system
- Reduces drift in terminology

## References

- Canonical vocabulary: `docs/architecture/canonical-terms.md`
