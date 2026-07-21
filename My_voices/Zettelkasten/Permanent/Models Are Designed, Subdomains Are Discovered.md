---
id: 20260721-1050
type: permanent
tags: [domain-driven-design, strategic-design, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Cotinuation of chapter 3 + chapt. 4_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Models Are Designed, Subdomains Are Discovered

A sharp distinction worth holding onto: **models are designed, while subdomains are discovered.**

- **Subdomains are discovered** — they already exist in the business. You don't invent them; you find them by analyzing the domain (see [[Business Domain and Subdomains]]).
- **Models are designed** — a [[Model as Abstraction|model]] is a deliberate choice about what to represent and what to leave out. There is no single "correct" model waiting to be found; you design one that usefully fits the problem.

This is also how you arrive at [[Bounded Context|bounded contexts]]: you can derive them from **semantics** — a conjunction of lexicographical words that carry a meaning in a given context. When those words are used inside that context, you have a bounded context there.

## Related

- [[Business Domain and Subdomains]] — the discovered side of the distinction.
- [[Model as Abstraction]] — the designed side of the distinction.
- [[Bounded Context]] — derived from the semantics of a context's language.
