---
id: 20260721-1010
type: permanent
tags: [domain-driven-design, strategic-design, business-logic]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Generic Subdomain

A **generic subdomain** handles logic that is general or common-sense — a business activity that others have already implemented many times before. It is still **complex**, but it provides **no business differentiation**: it needs no innovation or optimization to be competitive.

The defining decision for a generic subdomain is **buy or reuse, don't build**. Because the problem is already solved elsewhere, it is better to replicate an existing solution — for example, paying for or consuming a microservice that manages this part of the business — than to build it from the ground up. Spending your most valuable technical people here would be a waste; they belong on the [[Core Subdomain]].

Generic subdomains are also relatively **static** — they do not change and enhance constantly the way a core subdomain does, which is part of what makes an off-the-shelf or externally maintained solution safe to rely on.

Generic and supporting subdomains can intertwine: a [[Supporting Subdomain]] often leans on a generic, already-established service while still adding the company's own differentiation on top.

## Related

- [[Business Domain and Subdomains]] — the classification this type belongs to.
- [[Core Subdomain]] — the opposite: build in-house with your best people.
- [[Supporting Subdomain]] — differentiating but low-complexity; frequently built on generic services.
