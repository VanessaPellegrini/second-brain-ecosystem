# Vault Structure

A vault without structure becomes a junk drawer. A vault with too much structure becomes a prison.

The goal: **just enough structure to find things, not so much that it slows you down.**

## The PARA Method

The most popular organizing system for a Second Brain is **PARA**, created by Tiago Forte:

| Folder | What goes here | Example |
|--------|---------------|---------|
| **P**rojects | Active things with a deadline or goal | `launch-portfolio`, `thesis-2026` |
| **A**reas | Ongoing responsibilities with no end date | `health`, `finances`, `career` |
| **R**esources | Topics you're interested in | `machine-learning`, `design`, `cooking` |
| **A**rchive | Completed projects and inactive items | `old-project-2024` |

### How it looks in your vault:

```mermaid
graph TD
    Vault[📁 your-vault] --> P[📁 1-projects]
    Vault --> A[📁 2-areas]
    Vault --> R[📁 3-resources]
    Vault --> Arc[📁 4-archive]
    Vault --> D[📁 daily]
    Vault --> T[📁 templates]
    Vault --> H[📄 home.md]
    Vault -. optional .-> AI[📁 Librarian Layer<br/>raw · wiki · reports · reviews · memory · configs · .librarian]

    P --> P1[launch-portfolio.md]
    P --> P2[📁 thesis-2026]
    A --> A1[📁 health]
    A --> A2[📁 finances]
    A --> A3[📁 career]
    R --> R1[📁 machine-learning]
    R --> R2[📁 design]
    R --> R3[📁 cooking]
    Arc --> Arc1[📁 old-project-2024]
```

> 💡 The numbers (1-, 2-, 3-, 4-) keep folders in priority order in the file explorer.

## Optional AI Operational Layer: Librarian

**PARA organizes your life and projects. Librarian organizes the AI-processable knowledge layer.**

This layer is optional. Your Second Brain works without it. If you plan to use Librarian, add these folders at the vault root. They do not replace PARA: they live alongside it.

```text
vault/
  1-projects/
  2-areas/
  3-resources/
  4-archive/
  daily/
  inbox/
  templates/
  home.md

  raw/          # immutable sources approved for AI
  wiki/         # structured knowledge generated/curated by Librarian
  reports/      # automatic vault diagnostics
  reviews/      # proposals pending approval/rejection/editing
  memory/       # persistent agent/session memory
  configs/      # visible/editable Librarian configuration
  .librarian/   # internal state, indexes, cache, locks
```

The relationship between folders:

| Folder | Role | Who writes |
|--------|------|------------|
| `inbox/` | Temporary human capture | You |
| `raw/` | Sources approved for Librarian to read | You (explicit consent) |
| `wiki/` | Structured knowledge | Librarian |
| `reviews/` | Human-readable review and export surface | Librarian (you approve via CLI) |
| `reports/` | Vault diagnostics | Librarian |
| `memory/` | Agent continuity across sessions | Librarian |
| `configs/` | Explicit configuration rules | You |
| `.librarian/` | Internal technical state | Librarian |

Use `inbox/` for fast human capture. Move a source into `raw/` only when you want Librarian to process it. This separation acts as a consent boundary: not everything you capture automatically enters the AI layer.

Inside `wiki/`, Librarian expects this structure:

```text
wiki/
  index.md
  log.md
  conceptos/
  entidades/
  sources/
  synthesis/
```

`reviews/` is a human-readable review and export surface. `.librarian/proposals/` is the internal proposal source of truth. Before modifying the wiki, Librarian generates proposals that you review, approve, and apply via the CLI. The wiki is only modified through approve/apply. This keeps you in full control of your knowledge.

## The Home Note

Create a note called `home.md` and pin it as your opening note. This is your **dashboard** — the first thing you see when you open Obsidian.

```markdown
# 🏠 Home

## Active Projects
- [[launch-portfolio]] — Launch by June
- [[thesis-2026]] — First draft due April

## Quick Links
- [[reading-list]]
- [[weekly-review-template]]
- [[habits-tracker]]

## Today
![[{{date:YYYY-MM-DD}}]]
```

> To pin a note: right-click the tab → **"Pin"**. It stays open when you switch notes.

## Naming Conventions

Good naming makes everything searchable:

| Rule | Example |
|------|---------|
| Use lowercase with hyphens | `machine-learning.md`, not `Machine Learning.md` |
| Be descriptive | `interview-prep-questions.md`, not `notes2.md` |
| Date prefix for time-based notes | `2026-05-12-meeting-with-jane.md` |
| Use folders for grouping | `career/`, not 50 loose files |

## When in Doubt: Inbox

Not sure where a note goes? Create an `inbox/` folder. Dump things there and sort later during a weekly review.

```
📁 your-vault/
├── 📁 inbox/             ← Unsorted notes (sort weekly)
├── 📁 1-projects/
├── 📁 2-areas/
...
```

> The inbox is not a trash can. Clean it out weekly. If a note sits there for a month, archive it or delete it.

## The MOC (Map of Content)

As your vault grows, you'll want **MOCs** — index notes that link to related notes on a topic.

```markdown
# 🗺️ Machine Learning MOC

## Fundamentals
- [[what-is-machine-learning]]
- [[supervised-vs-unsupervised]]
- [[common-algorithms]]

## Courses
- [[andrew-ng-course-notes]]
- [[fast-ai-lectures]]

## Practice
- [[kaggle-projects]]
- [[ml-interview-prep]]
```

MOCs are like tables of contents for your brain. Start creating them when a topic has 5+ notes.

## Don't Overthink It

The perfect structure doesn't exist. Start with PARA, adjust as you go. Your vault will tell you what it needs after a few weeks of use.

**Principles over rules.**

## What's Next?

→ **[05 — Essential Plugins](./05-essential-plugins.md)**

---

[← 03 — Setting Up Obsidian](./03-setting-up-obsidian.md) · [Español](../es/04-vault-structure.md)
