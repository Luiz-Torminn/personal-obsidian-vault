---
id: 20260721-0940
type: permanent
tags: [domain-driven-design, backend, architecture]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Aggregate Root

The Aggregate Root is the single entry point — either an entity or a value object — through which all commands to an [[Aggregate]] must flow. It receives incoming requests and propagates the resulting changes throughout the aggregate's internal components.

The root is essential for maintaining strong consistency within the aggregate. Rather than allowing external systems to modify any part of the aggregate directly, all changes pass through the root. This single entry point lets the aggregate enforce all its business rules and invariants before accepting or rejecting a command.

The aggregate's **public interface** is defined by its root. When the root receives a command, it validates the input, ensures all relevant business rules hold, and orchestrates updates to the entities and value objects contained within the aggregate. Domain events are published through this same public interface, allowing external systems to react to significant state changes without coupling to the aggregate's internals.

## Related

- [[Aggregate]] — the whole that the root controls
- [[Aggregate Command]] — requests the root accepts
- [[Domain Event]] — messages the root publishes
