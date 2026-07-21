---
id: 20260721-1000
type: permanent
tags: [domain-driven-design, strategic-design, architecture, business-logic]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Business Domain and Subdomains

A **business domain** is the company's main area of activity. It is not implemented as one monolithic thing — it decomposes into **subdomains**, each a fine-grained instance of one aspect of the overall domain.

A subdomain is really a *finer-grained problem domain*: subdomains are derived from problems, and each one's goal is to provide solutions for a specific business capability. So the way to read a business is problem-first — the company faces problems, those problems carve the domain into subdomains, and each subdomain is the coherent slice of logic and activity that solves its problem.

Every subdomain falls into one of **three types**, which differ along three axes — how *complex* they are, whether they provide competitive *differentiation*, and how *dynamic* (frequently changing) they are:

- [[Core Subdomain]] — the competitive advantage; most complex and most dynamic.
- [[Supporting Subdomain]] — provides differentiation but is low in complexity.
- [[Generic Subdomain]] — a solved, common problem; complex but no differentiation.

Classifying each subdomain by type is what drives the big decisions: where to put your best people, and what to build versus buy.

```mermaid
flowchart TD
    D[Business Domain] --> S1[Subdomain]
    D --> S2[Subdomain]
    D --> S3[Subdomain]
    S1 --> Core["Core — competitive advantage · most complex · most dynamic"]
    S2 --> Sup["Supporting — differentiation · low complexity"]
    S3 --> Gen["Generic — solved elsewhere · buy or reuse"]
```

## Related

- [[Core Subdomain]] — the highest-value subdomain type; where to invest.
- [[Generic Subdomain]] — the buy/reuse type.
- [[Supporting Subdomain]] — the low-complexity, in-house-but-not-precious type.
- [[Subdomain Boundary Heuristics]] — how far to distill a domain into subdomains.
- [[Bounded Context]] — the language boundary layered on top of these problem boundaries.
