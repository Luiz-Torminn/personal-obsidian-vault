---
id: 20260721-0955
type: permanent
tags: [domain-driven-design, backend, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Domain Service

A Domain Service is a stateless object that holds business logic which does not naturally belong to any single [[Aggregate]] or [[Value Object]]. It represents an "orphan" piece of domain knowledge — logic that needs to exist but doesn't have a clear owner.

A Domain Service is typically implemented as a stateless, immutable object that orchestrates calls to various components of the system. It may combine knowledge from multiple aggregates, perform calculations that cut across domain concepts, or implement algorithms that are central to the business but don't fit cleanly into the model of any one aggregate.

Because Domain Services are stateless, they are simple to reason about and test. They depend on other domain objects (aggregates, value objects) but maintain no persistent state of their own. They are a pragmatic tool for expressing domain logic while keeping [[Aggregate]]s and value objects focused on their core responsibilities.

## Related

- [[Domain Model]] — part of the overall domain design
- [[Aggregate]] — may be orchestrated by or depend on a service
- [[Value Object]] — may be returned or used by a service
