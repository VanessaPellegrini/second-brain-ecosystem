# ADR 006: Index Invalidation Model

## Status

Accepted

## Context

The wiki index (`wiki/index.md`) and internal caches (semantic, wikilinks, backlinks, orphans) can become stale when files change externally — user edits in Obsidian, manual file operations, or external sync tools. Currently there is no mechanism to detect or recover from index staleness.

## Decision

Implement index metadata tracking and explicit rebuild. No filesystem watchers.

### Index Metadata

Location: `.librarian/index-metadata.json`

Tracks per-file: `mtimeMs`, `size`, `hash` (sha256). Tracks per-cache: `builtAt`, `status`.

### Status Model

| Status | Meaning | Action |
|--------|---------|--------|
| `fresh` | Index matches vault | Normal operation |
| `stale` | Changes detected | Warn, suggest rebuild |
| `missing` | No index exists | Block or require rebuild |
| `rebuilding` | Rebuild in progress | Wait |

### Invalidation Check

Runs when a command needs the index or when TUI starts. Not continuous.

Detects staleness by comparing current file state against stored metadata:
- Path added/removed → invalidates wikilinks, backlinks, orphans
- Content hash changed → invalidates semantic, wikilinks
- Size or mtime changed → triggers hash check

### Rebuild Command

```bash
librarian index rebuild
```

Full rebuild only in Sprint 2A. Walks `wiki/` and `raw/`, rebuilds all caches, sets status → `fresh`.

### Why No Watchers

Filesystem watchers multiply:
- Race conditions
- Invalidation bugs (partial events)
- Partial rebuilds (change during rebuild)
- Duplicate events
- Debounce complexity

The transactional base (ADR 004) must be solid before adding reactivity. Watchers belong to Sprint 2B+.

## Consequences

- Index staleness is detectable and observable
- Users can trigger rebuild explicitly
- TUI shows index status
- Operations can warn when working with stale data
- Foundation exists for future incremental rebuilds without changing the metadata model

## References

- Sprint 2A plan: `docs/sprint-2a-plan.md` section 4
- ADR 004: Transaction-like apply (index updates happen during apply)
