---
id: 20260721-1115
type: permanent
tags: [domain-driven-design, strategic-design, architecture]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Cotinuation of chapter 3 + chapt. 4_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Context Map

A **context map** is a **visual representation of the bounded contexts and their relationships** — how they coordinate and integrate with one another. It turns the abstract web of [[Bounded Context Integration (Contracts)|integrations]] (shared kernels, customer-supplier links, anti-corruption layers) into a single high-level picture.

It gives you two things at once:

- a **high-level design** view of the system's bounded contexts, and
- a holistic view of the **organizational / communication pairings** between the teams that own them.

Because it exposes both the technical and the team-communication structure, a context map is ideal to introduce **right from the get-go** of a project, rather than reconstructing it after the fact.

```mermaid
flowchart LR
    A[Context A] -->|Customer-Supplier| B[Context B]
    B -->|Shared Kernel| C[Context C]
    A -->|Anti-Corruption Layer| C
```

## Related

- [[Bounded Context]] — the units a context map lays out.
- [[Bounded Context Integration (Contracts)]] — the relationships a context map visualizes.
- [[Shared Kernel]] · [[Customer-Supplier (Upstream & Downstream)]] · [[Anti-Corruption Layer]] — the integration styles drawn on the map.
