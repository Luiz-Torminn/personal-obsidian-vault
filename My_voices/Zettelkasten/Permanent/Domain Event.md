---
id: 20260721-0950
type: permanent
tags: [domain-driven-design, backend, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Domain Event

A Domain Event is a message describing a significant event that has already occurred in the business domain. It communicates what has happened, enabling other parts of the system to react to state changes.

Domain Events are always named in the **past tense** — "OrderPlaced," "CustomerRegistered," "PaymentProcessed" — because they represent facts, not intentions. An event exists within the domain model itself and, like all domain concepts, it speaks the [[Ubiquitous Language]].

Domain Events are part of an [[Aggregate]]'s public interface. An aggregate publishes events through its [[Aggregate Root]] to signal meaningful changes. This allows external systems, other aggregates, and application services to respond without requiring direct coupling to the aggregate's internal structure. Events decouple systems while maintaining clarity about what happened in the business domain.

## Related

- [[Aggregate]] — the entity that publishes events
- [[Aggregate Root]] — the interface through which events are published
- [[Domain Service]] — may subscribe to or consume events
