---
id: 20260721-1030
type: permanent
tags: [domain-driven-design, strategic-design, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Domain Expert Mental Model

To discover domain knowledge, the developer first has to grasp a general understanding of the area the business operates in. The real goal, though, is deeper: to comprehend **how the domain expert thinks about the problem** — the expert's **mental model**.

Software should **mimic the domain expert's way of thinking**. The job of the software analyst is essentially to **translate that mental model into code**. For that translation to happen without loss, there must be clear, effective communication maintained *at all times* between the people involved.

This is why the [[Ubiquitous Language]] matters: it is the medium that lets the expert's mental model reach the code intact, instead of degrading through a chain of documents and hand-offs. From the mental model you distill a [[Model as Abstraction|model]] — the minimal representation the software actually implements.

## Related

- [[Ubiquitous Language]] — the shared vocabulary that carries the mental model into code.
- [[Model as Abstraction]] — the minimal representation distilled from the mental model.
- [[Agree on the Problem Before the Solution]] — the alignment that must precede translation.
