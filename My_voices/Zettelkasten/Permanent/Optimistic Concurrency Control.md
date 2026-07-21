---
id: 20260721-1000
type: permanent
tags: [domain-driven-design, backend, concurrency]
up: "[[* Domain-Driven Design MOC]]"
created: 2026-07-21
references:
  - Transcription file: Chapter 5 and 6_otter_ai_transcript.txt
  - Vlad Khononov, Learning Domain-Driven Design (O'Reilly, 2021), Part II: Tactical Design — Ch. 5–6. ISBN 978-1-098-10013-1
---

# Optimistic Concurrency Control

Optimistic Concurrency Control (OCC) prevents lost updates by verifying, at write time, that the state's version hasn't changed since it was read.

The flow: the caller reads the current value along with its version, and keeps/passes that version alongside any modification it makes to the loaded state. On write, the stored version must match the version originally read. If a concurrent transaction has already committed a change in the meantime, the later write is rejected — it has to reload and retry — rather than blindly overwriting the first transaction's commit.

This is a cross-cutting mechanism: it's the reasoning behind Transaction Script idempotency, and it's also the mechanism behind [[Aggregate]] consistency — it's how an aggregate stops a stale write from silently clobbering a newer one.

```mermaid
flowchart TD
    RD[Read state + version] --> MOD[Modify loaded state]
    MOD --> CMP{Stored version == version originally read?}
    CMP -->|Yes| WR[Write & increment version]
    CMP -->|No| REJ[Reject — concurrent update, reload & retry]
```

## Related

- [[Transaction Script]] — OCC is the mechanism behind its idempotency guarantee.
- [[Aggregate]] — OCC is the versioning mechanism that protects aggregate consistency under concurrent writes.
- [[Aggregate Command]] — the write pipeline that relies on OCC's version check before committing.
