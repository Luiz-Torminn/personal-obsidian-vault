---
id: 20260721-1035
type: permanent
tags: [domain-driven-design, strategic-design, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Model as Abstraction

A **model** is nothing more than a way to represent domain knowledge — specifically, the **minimal** representation of the knowledge distilled from the [[Domain Expert Mental Model|expert's mental model]].

The key property is that a model is an **abstraction**, and an abstraction is a representation that is **always correct but always incomplete**. You deliberately keep only the *minimum necessary* information to effectively fit what you are trying to achieve. Completeness is not the goal; usefulness is.

When building the model, applying this minimum-necessary discipline does **not** mean modeling only the happy paths. You must also take the **edge cases** into account — while still holding to the minimum-necessary approach for understanding and dealing with the problem.

## Related

- [[Domain Expert Mental Model]] — the source a model is distilled from.
- [[Ubiquitous Language]] — the shared vocabulary that makes a faithful model possible.
- [[Models Are Designed, Subdomains Are Discovered]] — a model is a deliberate design choice, not something found.
- [[Domain Model]] — the tactical pattern that implements a rich model in code.
