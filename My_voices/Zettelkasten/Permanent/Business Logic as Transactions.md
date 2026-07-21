---
id: 20260721-0905
type: permanent
tags: [domain-driven-design, backend, business-logic]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Business Logic as Transactions

At bottom, a business is a series of requests and responses between a client and a server. The client sends a request; the server processes it and returns a response. From the system's perspective, each transaction does one of three things: retrieves information the system manages, modifies it, or does both.

This is the foundational frame for understanding business logic—before you decide *how* to implement it, you recognize that you're building a handler for a transaction. The handler takes some input (often from a client), reads from and writes to the system's data store, applies whatever rules belong to that business operation, and produces an output.

Every implementation pattern for business logic—from the simplest to the most sophisticated—ultimately choreographs this same rhythm: receive → read → validate → modify → respond. The name "transaction script" comes from this model: each transaction is a script that orchestrates the flow.

## Related

- [[Transaction Script]] — the simplest pattern that scripts these transactions directly
- [[Active Record]] — a transaction acting through row-wrapping objects instead of imperative scripts