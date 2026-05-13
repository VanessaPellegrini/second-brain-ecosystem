# ADR 002: Consent Boundary Between inbox/ and raw/

## Status

Accepted

## Context

The vault has two folders that could be confused: `inbox/` (temporary human capture) and `raw/` (sources approved for AI processing). Without a clear boundary, users may not understand what data Librarian can access.

## Decision

`inbox/` and `raw/` are separated by a **consent boundary**:

- `inbox/` is for fast human capture. Librarian never reads from it.
- `raw/` is for sources explicitly approved for Librarian processing.
- Moving a file from `inbox/` to `raw/` is an intentional user action that grants consent.
- Nothing is automatically moved between these folders.

## Consequences

- Users maintain explicit control over what enters the AI layer
- The consent boundary is architectural, not just social
- Documentation consistently uses the term "explicit consent" when describing the `raw/` folder
- Automated tools must never move files into `raw/` without user action

## References

- Canonical vocabulary: `docs/architecture/canonical-terms.md`
- Vault structure guide: `second-brain/guides/en/04-vault-structure.md`
