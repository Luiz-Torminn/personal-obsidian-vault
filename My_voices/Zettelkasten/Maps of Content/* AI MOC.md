---
id: 20260602-0010
type: index
tags:
  - ai
  - computer-vision
  - machine-learning
  - moc
aliases:
  - AI MOC
  - AI Map of Content
up: "[[* Dev MOC]]"
---

# AI — Map of Content

> [!INFO] About this map
> A **Map of Content (MOC)** is a curated hub that gathers and gives context to the notes in a domain. Use it — not the folder tree — as your entry point to *AI*: start here and follow the links into each method.

The **AI** domain collects applied machine-learning knowledge. Its first cluster is **computer-vision post-processing** — what happens to detections *after* a model runs.

---

## Computer Vision — Post-Processing

When several detectors fire on the same image, their boxes overlap. Post-processing decides how to reconcile them.

- **[[Weighted Box Fusion (WBF)]]** — *combines* overlapping boxes to use evidence from all models.
- **[[Non-Maximum Suppression (NMS)]]** — *suppresses* (removes) overlapping boxes, keeping the highest-confidence one. *(stub)*

> [!NOTE]
> WBF and NMS are complementary: NMS can deduplicate a single model's predictions before WBF fuses across models.

---

## Tending this map

> [!TIP] Second-brain maintenance
> - Each note sets `up: "[[* AI MOC]]"`; this map links back down to it.
> - As new clusters appear (e.g. *Training*, *Evaluation Metrics*), add a section here or split into a sub-MOC.
> - Follow-ups live in [[Next Steps]]; topics to learn live in [[New Studies]].

---

## Related

- Up: [[* Dev MOC]]
- Down: [[Weighted Box Fusion (WBF)]] · [[Non-Maximum Suppression (NMS)]]
