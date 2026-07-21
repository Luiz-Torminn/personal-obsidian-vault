---
id: 20260721-1005
type: permanent
tags: [domain-driven-design, strategic-design, business-logic, competitive-advantage]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Domain-Driven Design (Chap. 1 to 3)_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part I: Strategic Design — Ch. 1–4. ISBN 978-1-098-10013-1
---

# Core Subdomain

The **core subdomain** is the subdomain responsible for the company's **competitive advantage** — the area where the company generates most, if not all, of its revenue. It is the most important of the three [[Business Domain and Subdomains|subdomain types]], and also the **most complex**.

Because it is the source of advantage, a core subdomain is typically something the company does *not* want competitors to copy. That has direct consequences for how you build it:

- **Assign your best people.** The most experienced and most valuable engineers should be working on the core subdomain, not on generic or supporting ones.
- **Build it in-house; don't cut corners.** It has to support the company long-term and stay reliable, independent of other services and outside companies. Reaching for a simple procedural pattern here is a mistake — its complexity is exactly why a [[Transaction Script]] should never be used for a core subdomain.
- **Expect constant change.** The core subdomain is the most *dynamic* type: it is always being updated, enhanced, and extended with new logic. This dynamism is why keeping ownership and control in-house matters.

The core subdomain also shapes integration decisions: when a downstream context holds a core subdomain, that is one of the reasons to protect it with an [[Anti-Corruption Layer]] rather than conform to an external model.

## Related

- [[Business Domain and Subdomains]] — the classification this type belongs to.
- [[Generic Subdomain]] — the opposite trade-off: complex but no differentiation, so buy it.
- [[Supporting Subdomain]] — provides differentiation too, but at low complexity.
- [[Anti-Corruption Layer]] — a core subdomain downstream is a reason to shield it from foreign models.
