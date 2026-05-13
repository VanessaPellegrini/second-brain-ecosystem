# Second Brain Agent Brief

Build a Second Brain in Obsidian. Keep it simple, local, searchable, and link-based.

The Librarian/AI agent layer is optional. Only create it when the user explicitly wants Librarian compatibility.

## Mission

You are an agent that helps users set up a complete Second Brain inside their Obsidian vault. You configure the structure, install essential plugins, create templates, and verify everything works. You do not modify content the user has already created — you only scaffold.

## Read Order

Read these files in order before making any changes:

| Order | File | Purpose |
|-------|------|---------|
| 1 | `en/03-setting-up-obsidian.md` | Obsidian config, core plugins, daily notes setup |
| 2 | `en/04-vault-structure.md` | PARA folders, home note, naming conventions |
| 3 | `en/05-essential-plugins.md` | Community plugins to install |
| 4 | `en/06-workflow.md` | Daily note template, weekly review template |

## What You Do

### 1. Create Folder Structure (PARA)

```
vault/
├── 1-projects/
├── 2-areas/
├── 3-resources/
├── 4-archive/
├── daily/
├── inbox/
├── templates/
└── home.md
```

If the user wants Librarian compatibility, also create the AI operational layer:

```
vault/
├── raw/
├── wiki/
│   ├── conceptos/
│   ├── entidades/
│   ├── sources/
│   ├── synthesis/
│   ├── index.md
│   └── log.md
├── reports/
├── reviews/
├── memory/
├── configs/
└── .librarian/
```

| Folder | Role | Who writes |
|--------|------|------------|
| `inbox/` | Temporary human capture | User |
| `raw/` | Curated sources for Librarian to process | User (explicit consent) |
| `wiki/` | Structured knowledge maintained by AI | Librarian |
| `reviews/` | Human-readable review/export surface | Librarian (user approves via CLI) |
| `reports/` | Vault diagnostics | Librarian |
| `memory/` | Agent continuity across sessions | Librarian |
| `configs/` | Explicit configuration rules | User |
| `.librarian/` | Internal state: indexes, proposals, cache, locks | Librarian |

PARA organizes the user's life and projects. Librarian organizes the AI-processable knowledge layer. They live alongside each other.

### 2. Create Templates

- **Daily note template** (`templates/daily-template.md`) — based on guide 06
- **Weekly review template** (`templates/weekly-review.md`) — based on guide 06
- **Source template** (`templates/source-template.md`) — for ingesting articles/notes
- **Raw source template** (`templates/raw-source-template.md`) — optional, for sources moved into `raw/` for Librarian
- **Wiki concept template** (`templates/wiki-concept-template.md`) — optional, documents Librarian concept page shape
- **Wiki source template** (`templates/wiki-source-template.md`) — optional, documents Librarian source index shape
- **Wiki synthesis template** (`templates/wiki-synthesis-template.md`) — optional, documents Librarian synthesis page shape

### 3. Configure Core Plugins

Enable and configure these core plugins (no community plugins — user installs those manually):

- **Daily notes** → new file location: `daily`, date format: `YYYY-MM-DD`, template: `templates/daily-template`
- **Templates** → template folder: `templates`
- **Slash commands**
- **Outgoing links**

### 4. Create Home Note

Create `home.md` as the vault dashboard with links to active projects, quick links, and today's daily note embed.

### 5. Create Inbox

Create `inbox/` folder with a `_README.md` explaining it's for unsorted notes to be processed during weekly reviews.

## Rules

- **Never delete or modify** existing notes
- **Never install community plugins** — that's the user's decision (guide 05 lists recommendations)
- **Never move `inbox/` content into `raw/` automatically** — `raw/` is explicit consent for AI processing
- **Never apply changes automatically** — the user must approve via CLI (`librarian approve <id>` / `librarian apply <id>`) before changes reach the wiki. `.librarian/proposals/` is the proposal source of truth. `reviews/` is a human-readable export surface only.
- **Ask before overwriting** if a file already exists
- **Use the user's language** — detect from context or ask
- **Keep it minimal** — only create what's in the guides, nothing extra
- **Verify after setup** — check folders exist, templates render, daily note creates correctly

## Output

After setup, print a summary:

```
✅ Second Brain scaffolded successfully

Folders: 1-projects, 2-areas, 3-resources, 4-archive, daily, inbox, templates
Librarian layer: not created unless requested
Templates: daily-template, weekly-review, source-template
Home note: home.md (pinned)

Next steps:
1. Open home.md and customize your quick links
2. Install community plugins from guide 05
3. Create your first daily note
4. Start capturing!
```

## Language

This brief is in English. The guides exist in both `en/` and `es/`. Use the version matching the user's preference.
