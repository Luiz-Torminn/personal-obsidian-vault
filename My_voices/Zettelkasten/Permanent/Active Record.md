---
id: 20260721-0915
type: permanent
tags: [domain-driven-design, backend, design-patterns, database]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Active Record

An Active Record is an object that wraps a single row in a database table or view. It encapsulates two responsibilities: mapping the in-memory object to the database schema, and persistence—including the ability to carry domain logic and validation for that row's data.

The key distinction from a plain transaction script is *where* the logic lives. A transaction script sits between the consumer and the provider, accepting a request, transforming data, and returning a response. An Active Record, by contrast, sits *at the provider layer*—it *is* the row, enriched with methods and validation. When you modify an Active Record instance, you're modifying a thing that knows how to persist itself.

This means validation happens at a granular scope: row-level, within a schema. Before saving a row, the Active Record validates that its data meets the constraints of the domain—not at some earlier transformation step, but right where the data lives. The transaction itself still completes atomically (all or nothing), but the logic is distributed among the objects that represent the data.

Active Record is still a simple-logic pattern—it doesn't model complex business processes or aggregate roots. But it is more structured than a pure script: domain knowledge lives in the objects themselves, not scattered across procedures.

## Related

- [[Transaction Script]] — contrast: the simpler pattern that handles transactions via imperative scripts
- [[Domain Model]] — a richer pattern that models complex domain concepts and their relationships
- [[Relational Database Fundamentals]] — the table structure that Active Records wrap