# Plugins Esenciales

Obsidian es poderoso por sí solo. Los plugins lo hacen *tuyo*.

Los plugins comunitarios extienden Obsidian con funciones que la app core no tiene. Hay más de 1,000 — pero solo necesitás un puñado para empezar.

## Cómo Instalar Plugins Comunitarios

1. Andá a **Settings → Community plugins**
2. Clickeá **"Turn on community plugins"** (vas a ver un warning sobre código de terceros — es normal)
3. Clickeá **"Browse"** para abrir el marketplace de plugins
4. Buscá el nombre del plugin → Clickeá **"Install"** → Clickeá **"Enable"**

> 💡 Después de instalar plugins, podés configurar cada uno cliqueando el ⚙️ engranaje al lado de su nombre en la lista de Community plugins.

## El Pack Inicial

Estos 8 plugins cubren el 90% de lo que necesitás:

### 1. 📅 Calendar

Agrega un widget de calendario a tu sidebar. Cliqueá cualquier día para crear/abrir su nota diaria.

- **Buscar:** `calendar`
- **Configurar:** Nada — funciona solo

### 2. ✅ Tasks

Potencia tus checkboxes con fechas de vencimiento, recurrencia, prioridades y filtros.

```markdown
- [ ] Comprar provisiones 📅 2026-05-15
- [ ] Revisión semanal 🔁 every week on Friday ⏫
- [x] Mandar email ✅ 2026-05-12
```

- **Buscar:** `obsidian-checklist-plugin` o `tasks`
- **Configurar:** Elegí tus preferencias de formato de tareas en la config del plugin

### 3. 🔗 Dataview

Consultá tu vault como una base de datos. Creá listas, tablas y vistas dinámicas.

```dataview
TASK FROM "1-proyectos"
WHERE !completed
SORT due ASC
```

- **Buscar:** `dataview`
- **Configurar:** Habilitá JavaScript queries si querés potencia avanzada (opcional)
- **Cuándo agregar:** Cuando tengas 50+ notas con metadatos

### 4. 🎨 Excalidraw

Dibujá diagramas, sketches y notas visuales directamente en Obsidian. Perfecto para pensadores visuales.

- **Buscar:** `obsidian-excalidraw-plugin`
- **Configurar:** Elegí tus valores default de dibujo

### 5. 📝 Templater

Templates avanzados con variables, formato de fechas y contenido dinámico. Mucho más poderoso que el plugin core de Templates.

```markdown
---
created: {{date:YYYY-MM-DD}}
tags: [<% tp.file.tags() %>]
---

# {{title}}

## Notas
```

- **Buscar:** `templater-obsidian`
- **Configurar:** Poné tu carpeta de templates en `templates/`

Este repo incluye templates iniciales en [`second-brain/templates/`](../../templates/): nota diaria, revisión semanal, fuente, fuente para `raw/` y páginas base para `wiki/` de Librarian.

### 6. 🏷️ Tag Wrangler

Renombrá, mergeá y gestioná tags directamente desde el panel de tags. No más editar tags manualmente nota por nota.

- **Buscar:** `tag-wrangler`
- **Configurar:** Nada

### 7. 🧹 Linter

Formateá y limpiá tu Markdown automáticamente. Estilo consistente sin pensar.

- **Buscar:** `obsidian-linter`
- **Configurar:** Habilitá las reglas que te importen (espacios trailing, YAML frontmatter, etc.)

### 8. 📊 Homepage

Abrí una nota específica cada vez que lanzás Obsidian. Combina perfecto con la nota `home.md` de la guía anterior.

- **Buscar:** `homepage`
- **Configurar:** Poné tu nota de home en `home`

## Power-Ups Opcionales

Agregá estos cuando sientas la necesidad:

| Plugin | Qué hace | Cuándo agregar |
|--------|----------|----------------|
| **Readwise Official** | Sincronizar highlights de Kindle, artículos, tweets | Cuando uses Readwise |
| **Omnivore** | Guardar y sincronizar artículos web | Cuando leás mucho online |
| **Kanban** | Tableros visuales de tareas dentro de Obsidian | Cuando necesites tracking de proyectos |
| **Periodic Notes** | Notas semanales y mensuales (más allá de las diarias) | Cuando las notas diarias no alcancen |
| **Quick Add** | Captura rápida de notas con templates | Cuando capturar se sienta lento |
| **Auto Link Title** | Buscar automáticamente títulos para URLs pegadas | Cuando pegues muchos links |

## La Trampa de los Plugins

> ⚠️ **No instales 30 plugins el primer día.** Vas a pasar más tiempo configurando que usando tu Segundo Cerebro.

Empezá con el **Pack Inicial**. Agregá más solo cuando pienses "Ojalá pudiera hacer X" — entonces buscá un plugin que haga X.

## ¿Qué sigue?

→ **[06 — Tu flujo de trabajo](./06-workflow.md)**

---

[← 04 — Estructura del Vault](./04-vault-structure.md) · [English](../en/05-essential-plugins.md)
