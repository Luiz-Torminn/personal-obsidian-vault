---
id: 20260721-0930
type: permanent
tags: [domain-driven-design, backend, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Entity

An Entity is a mutable object composed of multiple value objects, identified uniquely by an ID rather than by the values it contains. The ID is non-replicable and remains stable across the entity's lifetime.

What makes an entity fundamentally different from a value object is that it is **mutable**. You can change its properties, and it remains the same entity — the ID persists. Two entities with identical property values are not duplicates; they can be distinct instances that merely happen to share values. If you change a property on an entity, you don't create a new instance; you modify the existing one.

An entity is never implemented in isolation. It always exists within the context of an [[Aggregate]], which provides its structural and transactional boundaries. The aggregate determines how the entity can be accessed and modified from outside.

## Related

- [[Value Object]] — the opposite conceptually: immutable, identified by values
- [[Aggregate]] — the container that gives entities meaning and transactional semantics
- [[Domain Model]] — entities are the building blocks of the domain model
- [[Database Keys and Identity]] — how identity maps to persistence
