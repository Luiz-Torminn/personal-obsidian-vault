---
id: 20260721-0925
type: permanent
tags: [domain-driven-design, backend, design]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Value Object

A Value Object is a fine-grained, immutable object that is identified not by a separate ID, but by the composite of its property values. Change any property, and you have a new Value Object. Two Value Objects with the same property values are duplicates—indistinguishable and therefore equal.

The immutability is the core characteristic. Once constructed, a Value Object cannot change. If you need a different value, you construct a new instance. This design has profound consequences: it eliminates entire categories of subtle bugs (shared mutable state, unexpected mutations at a distance) and makes reasoning about equality straightforward (just compare values).

Validation typically uses the language's primitive types (string, integer, boolean, and so on), though a Value Object may also compose other Value Objects. The real power comes from *where* validation happens: on construction. When you create a Value Object, you ensure its properties are valid *immediately*. There's no separate validation call, no transient invalid state. This pushes validation to the point of use, which reinforces the ubiquitous language—a property gets a clear, meaningful type and name, and that name and type become part of how the domain speaks about itself.

This is the best way to avoid duplicating validation logic across a system. Instead of checking an email format or a phone number format in a transaction script, in a service layer, and in a presentation layer, you encode that validation once in a Value Object. Every place that needs that data type uses the same Value Object, and every place that uses it gets validation "for free" at the moment of construction.

## Related

- [[Entity]] — contrast: identity-by-value and immutable versus identity-by-ID and mutable
- [[Domain Model]] — Value Objects are building blocks within domain models