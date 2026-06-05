---
id: 20260604-0001
type: index
tags: [meta, specs, conventions, moc]
aliases: [Vault Specs, Conventions, Style Guide]
up: "[[Home]]"
---

# VAULT_SPECS — How this Zettelkasten works

> [!INFO] Purpose
> The single source of truth for **how to take notes in this vault**. Anyone using it as a second brain should read this before adding content. If a rule here ever conflicts with a note, this file wins — update the note.

Entry point: **[[Home]]**.

---

## 1. Philosophy

This is a **Zettelkasten** (German for "slip box"): a network of small, atomic notes connected by links. You navigate by **links and Maps of Content (MOCs)** — *not* by the folder tree. Folders only group notes by **lifecycle type** (`Permanent/`, `Maps of Content/`), never by topic; the real structure lives in the links.

A note moves through a **lifecycle**:

```
fleeting  ──promote──►  permanent  ──organized by──►  index (MOC)
(capture)               (your knowledge)               (navigation)
```

- **Fleeting** — raw, temporary capture. Lives in `+ Inbox/`. Processed and then deleted.
- **Permanent** — one idea, written in your own words, densely linked. The heart of the vault.
- **Index** — a structure note (MOC, Home, Next Steps, New Studies) that gathers and gives context to other notes.

**Golden rules**
1. One note = one idea (atomic).
2. Write in your own words; link generously.
3. Every note points **up** to a parent map; every map points **down** to its notes (two-way).
4. Keep filenames human-readable; the unique ID lives in the frontmatter.

---

## 2. Folder layout

Notes are grouped by **lifecycle type**, not by topic. The root holds the entry points and the capture layer; two sub-folders hold the body of notes:

```
Zettelkasten/
├── Home.md                 ← start here (the dashboard)
├── VAULT_SPECS.md          ← this file
├── Next Steps.md           ← actionable follow-ups (refine existing notes)
├── New Studies.md          ← backlog of topics to learn from scratch
├── + Inbox/                ← fleeting notes, one per idea (transient)
│   └── How to use the Inbox.md
├── Maps of Content/        ← index notes (MOCs) — '*' sorts them to the top
│   ├── * Business MOC.md
│   ├── * Dev MOC.md
│   ├── * AI MOC.md
│   └── * Database MOC.md
├── Permanent/              ← atomic concept notes (the heart of the vault)
│   ├── Database Normalization.md
│   ├── Business Plan.md
│   └── ...
└── images/                 ← all image attachments
```

- **Root** — `Home`, `VAULT_SPECS`, and the capture layer (`Next Steps`, `New Studies`, `+ Inbox/`). These are the pages you open directly.
- **`Maps of Content/`** — every `* X MOC` index note.
- **`Permanent/`** — every `type: permanent` note.

> [!WARNING] Group by type, never by topic
> Sort notes by lifecycle (`Permanent/`, `Maps of Content/`) only. Do **not** nest by subject (`Permanent/Database/`, `Permanent/Business/`, …). Atomicity + links + MOCs replace topical hierarchy — and because links resolve by name, a note can move between these type-folders without breaking anything.

---

## 3. Note types & property schema

Frontmatter (YAML properties) is required. Use these keys consistently:

| Key       | Required        | Meaning                                                        |
| --------- | --------------- | -------------------------------------------------------------- |
| `id`      | yes             | Unique identifier, format `YYYYMMDD-HHMM` (creation time).     |
| `type`    | yes             | Lifecycle: `fleeting` \| `permanent` \| `index`.               |
| `tags`    | yes (perm/idx)  | Inline list, lowercase-kebab: `[database, design]`.            |
| `up`      | yes (except Home)| Wikilink to the parent map: `"[[* Database MOC]]"`.           |
| `created` | yes             | `YYYY-MM-DD`.                                                  |
| `aliases` | optional        | Alternative names (common on MOCs): `[Database MOC]`.          |
| `references` | optional     | Source material the note derives from (books, papers, courses, URLs). YAML list. |

**`type` values**
- `fleeting` — inbox capture. Minimal frontmatter (`id`, `type`, `created`). No `up` needed.
- `permanent` — an atomic concept note. Always sets `up:` to its domain MOC.
- `index` — a structure note: MOCs, `Home`, `Next Steps`, `New Studies`, this file.

### Templates (copy-paste)

**Permanent note**
```yaml
---
id: 20260604-1530
type: permanent
tags: [topic, subtopic]
up: "[[* Database MOC]]"
created: 2026-06-04
references:                       # optional — source material the note derives from
  - Book / paper / course / URL
---
# Title

One idea, in your own words. Link to related notes like [[Other Note]].

## Related
- Lateral links to sibling notes (the parent is already in `up:`).
```

> [!TIP] Tracking sources
> Use `references` to record where a note's material comes from. It's a list, so add one item per source. Example — the business notes derive from the *Harvard Business Review Entrepreneur's Handbook*. Omit the key entirely for notes with no external source.

**Index note (MOC)**
```yaml
---
id: 20260604-1531
type: index
tags: [domain, moc]
aliases: [Domain MOC]
up: "[[* Parent MOC]]"   # or [[Home]] for a domain MOC
---
# Domain — Map of Content

> [!INFO] About this map
> Curated entry point to the domain.

## <sections grouping child notes>
- [[Child Note]] — one-line context.

## Related
- Up: [[* Parent MOC]]
- Down: [[Child Note]] · ...
```

**Fleeting note**
```yaml
---
id: 20260604-1532
type: fleeting
tags: [inbox]
created: 2026-06-04
---
Raw thought. Process later (see [[How to use the Inbox]]).
```

---

## 4. Naming conventions

- **Filenames**: human-readable Title Case — `Database Normalization.md`. This is the link target.
- **MOCs**: prefix with `* ` and suffix with `MOC` → `* Database MOC.md`, kept in `Maps of Content/`. The `*` floats them to the top of the file list; the unique title keeps every name distinct.
- **IDs**: `YYYYMMDD-HHMM` (e.g. `20260604-1530`). Stable — never change an `id` after creation.
- **Tags**: lowercase, kebab-case, no `#` in frontmatter → `competitive-advantage`.
- **Images**: keep originals in `images/`; embed by name only.

---

## 5. Linking rules

- **Link by name, never by path**: `[[Database Normalization]]`. Obsidian resolves names regardless of folder, so links survive moves.
- **Aliased links**: `[[* Database MOC|Database]]` shows "Database" but targets the MOC.
- **Block / heading links**: `[[Note#Heading]]` or `[[Note#^blockid]]` for precise references.
- **Embeds**: `![[image.png]]` for images, `![[Note#Heading]]` to transclude.
- **Two-way navigation is mandatory**:
  - every `permanent` note sets `up:` to its MOC;
  - every MOC lists that note under a section **and** in its `## Related → Down:` line.
- `## Related` in a permanent note is for **lateral** links (siblings, "see also"). The parent already lives in `up:` — don't duplicate it there.

---

## 6. Workflow — adding knowledge

```
capture → process → promote → file → link → log follow-ups
```

1. **Capture** a thought as a `fleeting` note in `+ Inbox/` (see [[*How to use the Inbox]]).
2. **Process** the Inbox regularly. For each note: promote, defer to [[New Studies]], or discard.
3. **Promote** to a `permanent` note: rewrite in your own words, add the full frontmatter, then **delete the fleeting note**.
4. **File** it: set `up:` to the right MOC, and add it to that MOC's body + `Down:` line.
5. **Link** it to related notes already in the vault.
6. **Log follow-ups**: refinements go in [[Next Steps]]; new topics to learn go in [[New Studies]].

> [!TIP] Tending the maps
> A MOC is only useful while current. When a section of a MOC outgrows itself, promote it into its own `* Sub MOC` and link it from the parent. When a brand-new area appears, add its MOC under **Domains** in [[Home]].

---

## 7. Worked example — adding a note end-to-end

You learn about database **transactions**.

1. **Capture** — `+ Inbox/transactions ACID?.md` (`type: fleeting`): *"ACID — atomicity, consistency, isolation, durability. Relates to constraints?"*
2. **Promote** — create `Permanent/Transactions.md`:
   ```yaml
   ---
   id: 20260605-0900
   type: permanent
   tags: [database, sql, transactions]
   up: "[[* Database MOC]]"
   created: 2026-06-05
   ---
   # Transactions
   A transaction groups statements into one atomic unit (ACID)...
   Builds on [[SQL Language Concepts]] and [[Relational Database Fundamentals]].
   ```
   Then delete the fleeting note.
3. **File** — in `Maps of Content/* Database MOC.md`, add under *Atomic Concepts*:
   `- [[Transactions]] — grouping statements atomically (ACID).`
   and append `[[Transactions]]` to its `Down:` line.
4. **Log** — add to [[Next Steps]]: `- [ ] Add isolation-level examples to [[Transactions]].`

Done — the note is atomic, two-way linked, discoverable from [[Home]] → Database, and its follow-up is tracked.

---

## Related

- Up: [[Home]]
- Workflow notes: [[Next Steps]] · [[New Studies]] · [[*How to use the Inbox]]
