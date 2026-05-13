# Essential Plugins

Obsidian is powerful on its own. Plugins make it *yours*.

Community plugins extend Obsidian with features the core app doesn't have. There are over 1,000 of them — but you only need a handful to start.

## How to Install Community Plugins

1. Go to **Settings → Community plugins**
2. Click **"Turn on community plugins"** (you'll see a warning about third-party code — that's normal)
3. Click **"Browse"** to open the plugin marketplace
4. Search for a plugin name → Click **"Install"** → Click **"Enable"**

> 💡 After installing plugins, you can configure each one by clicking the ⚙️ gear next to its name in the Community plugins list.

## The Starter Pack

These 8 plugins will cover 90% of your needs:

### 1. 📅 Calendar

Adds a calendar widget to your sidebar. Click any day to create/open its daily note.

- **Search for:** `calendar`
- **Configure:** Nothing needed — it just works

### 2. ✅ Tasks

Supercharges your checkboxes with due dates, recurrence, priorities, and filtering.

```markdown
- [ ] Buy groceries 📅 2026-05-15
- [ ] Weekly review 🔁 every week on Friday ⏫
- [x] Send email ✅ 2026-05-12
```

- **Search for:** `obsidian-checklist-plugin` or `tasks`
- **Configure:** Set your task format preferences in the plugin settings

### 3. 🔗 Dataview

Query your vault like a database. Create dynamic lists, tables, and views.

```dataview
TASK FROM "1-projects"
WHERE !completed
SORT due ASC
```

- **Search for:** `dataview`
- **Configure:** Enable JavaScript queries if you want advanced power (optional)
- **When to add:** When you have 50+ notes with metadata

### 4. 🎨 Excalidraw

Draw diagrams, sketches, and visual notes right inside Obsidian. Perfect for visual thinkers.

- **Search for:** `obsidian-excalidraw-plugin`
- **Configure:** Set your preferred drawing defaults

### 5. 📝 Templater

Advanced templates with variables, date formatting, and dynamic content. Way more powerful than the core Templates plugin.

```markdown
---
created: {{date:YYYY-MM-DD}}
tags: [<% tp.file.tags() %>]
---

# {{title}}

## Notes
```

- **Search for:** `templater-obsidian`
- **Configure:** Set your templates folder to `templates/`

This repo includes starter templates in [`second-brain/templates/`](../../templates/): daily note, weekly review, source note, `raw/` source, base `wiki/` pages for Librarian, and templates for `reviews/` and `reports/`.

### 6. 🏷️ Tag Wrangler

Rename, merge, and manage tags directly from the tag pane. No more manually editing tags one note at a time.

- **Search for:** `tag-wrangler`
- **Configure:** Nothing needed

### 7. 🧹 Linter

Automatically format and clean up your Markdown. Consistent style without thinking about it.

- **Search for:** `obsidian-linter`
- **Configure:** Enable the rules you care about (trailing spaces, YAML frontmatter, etc.)

### 8. 📊 Homepage

Open a specific note every time you launch Obsidian. Pairs perfectly with the `home.md` note from the previous guide.

- **Search for:** `homepage`
- **Configure:** Set your homepage note to `home`

## Optional Power-Ups

Add these when you feel the need:

| Plugin | What it does | When to add |
|--------|-------------|-------------|
| **Readwise Official** | Sync highlights from Kindle, articles, tweets | When you use Readwise |
| **Omnivore** | Save and sync web articles | When you read lots online |
| **Kanban** | Visual task boards inside Obsidian | When you need project tracking |
| **Periodic Notes** | Weekly and monthly notes (beyond daily) | When daily notes aren't enough |
| **Quick Add** | Rapid note capture with templates | When capture feels slow |
| **Auto Link Title** | Automatically fetch titles for pasted URLs | When you paste lots of links |

## The Plugin Trap

> ⚠️ **Don't install 30 plugins on day one.** You'll spend more time configuring than actually using your Second Brain.

Start with the **Starter Pack**. Add more only when you think "I wish I could do X" — then search for a plugin that does X.

## What's Next?

→ **[06 — Your Workflow](./06-workflow.md)**

---

[← 04 — Vault Structure](./04-vault-structure.md) · [Español](../es/05-essential-plugins.md)
