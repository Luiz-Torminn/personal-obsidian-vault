---
id: 20260721-1015
type: permanent
tags: [domain-driven-design, strategic-design, business-logic]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Supporting Subdomain

A **supporting subdomain** offers some **business differentiation** but has **lower complexity** than either the core or generic types. It matters to the company's edge, yet the problems it solves are not hard.

The trade-off it creates: because it is differentiating, it usually cannot simply be bought — most of the time it must be developed in-house. But because it is low-complexity, the solutions involved are low-level, so it is **not worth spending your best, most valuable technical people** on it. That talent is better assigned to the [[Core Subdomain]].

Supporting and generic subdomains often **intertwine**: a supporting subdomain may reuse a [[Generic Subdomain|generic]], already-established service or pipeline and still deliver the company's own differentiation on top of it. Like generic subdomains, supporting ones are relatively static compared with the constantly-changing core.

## Related

- [[Business Domain and Subdomains]] — the classification this type belongs to.
- [[Generic Subdomain]] — often reused underneath a supporting subdomain.
- [[Core Subdomain]] — where your top talent should go instead.
