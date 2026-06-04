---
id: 20260601-0010
type: index
tags: [development, database, architecture, moc]
aliases: [Database MOC, Database Map of Content]
up: "[[* Dev MOC]]"
---

# Database — Map of Content

> [!INFO] About this map
> A **Map of Content (MOC)** is a curated hub that gathers and gives context to the notes in a domain. Use it — not the folder tree — as your entry point to *Database*: start here, follow the links, and let the structure guide your thinking.

The central hub for designing robust relational database systems — from first principles to schema, integrity, and security.

---

## Core Philosophy

The primary goals of a well-designed database are:

- **Consistency** — no internal conflicts (e.g. linking data via Foreign Keys).
- **Integrity** — data must be accurate, complete, and follow business rules.
- **Maintainability** — naming conventions make the schema easy to update and expand.
- **Performance** — optimization via [[SQL Data Types]] and [[Indexing|indexing]].
- **Security** — preventing leaks through [[Encryption]] and [[SQL Access Control]].
- **Scalability & Flexibility** — handle more users and adapt to change.

---

## The Design Workflow

1. [[Database Design Process]] — a step-by-step guide from requirements to implementation.
2. [[Relational Database Fundamentals]] — tables, Foreign Keys, and joins.
3. [[Database Normalization|Normalization]] — reduce redundancy and improve integrity via normal forms.
4. [[Relationship Mapping]] — define relationships and cardinality.

---

## Atomic Concepts

- [[Relationship Mapping]] — cardinality and entity connections.
- [[Database Keys and Identity]] — candidate keys, IDs, and Primary Keys.
- [[SQL Data Types]] — choosing between `CHAR`, `VARCHAR`, `INT`, etc.
- [[SQL Language Concepts]] — declarative SQL mindset, constraints, and referential actions.
- [[SQL Access Control]] — roles, permissions, and least-privilege patterns.
- [[Encryption]] — hashing vs. reversible encryption for protecting sensitive data.
- [[Indexing]] — B-tree and full-text indexes for read performance. *(stub)*

---

## Tending this map

> [!TIP] Second-brain maintenance
> - Add a note here the moment it belongs to *Database* — a MOC is only useful while it stays current.
> - Link bidirectionally: every note sets `up: "[[* Database MOC]]"`, and this MOC links back to it.
> - Active follow-ups live in [[Next Steps]]; unexplored topics live in [[New Studies]].
> - When a cluster outgrows a section, promote it into its own sub-MOC and link it from here.

---

## Related

- Up: [[* Dev MOC]]
- Follow-ups: [[Next Steps]] · Backlog: [[New Studies]]
