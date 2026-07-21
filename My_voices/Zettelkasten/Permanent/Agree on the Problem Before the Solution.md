---
id: 20260721-1040
type: permanent
tags: [domain-driven-design, strategic-design, management]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Agree on the Problem Before the Solution

Before any software gets built, everyone has to be **on the same page** — level with the same vision and understanding the same things. Alignment is a prerequisite, not a by-product.

The sequence is explicit:

> We must first agree on the problem, then we agree on the solution, and finally we implement the solution.

Concretely, for a project to succeed, all stakeholders must agree on three things: the **problem** being solved, the **solution** being built for it, and both the **functional and non-functional requirements** of that solution. Skipping the agreement on the problem and jumping to a solution is how projects diverge — everyone builds toward a different unstated goal.

This alignment is what a clear, continuous communication channel is *for*, and it is the human precondition that makes the [[Ubiquitous Language]] and faithful translation of the [[Domain Expert Mental Model]] possible.

```mermaid
flowchart LR
    A[Agree on the problem] --> B[Agree on the solution] --> C[Implement the solution]
```

## Related

- [[Ubiquitous Language]] — the shared vocabulary that keeps the agreement intact.
- [[Domain Expert Mental Model]] — what the team is aligning around.
