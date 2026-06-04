---
epoch: 1780415658137
modelKey: "gpt-5.2|github-copilot"
topic: "Annotate Code With Mental Models"



tags:
  - copilot-conversation
---

**user**: For the Incremental code example (logic flow) section, add a comment to indicate the respective mental model parts (and subparts)  that each part of the code represents - with pointing references for each in the text
[Context: Notes: Estudos/Dev/AI/Computer Vision/Post Processing/Weighted Box Fusion (WBF).md]
[Timestamp: 2026/06/02 12:54:18]

**ai**: ## Incremental code example (logic flow) — with mental-model pointers

```python
from collections import defaultdict

# (Mental model §3) Uses IoU to decide whether two boxes refer to the same object instance
#   - “Identify which boxes refer to the same object instance … using IoU”
def iou(box_a, box_b):
    # box format: [score, x1, y1, x2, y2]  (Mental model §1: model outputs, after stripping label)
    _, ax1, ay1, ax2, ay2 = box_a
    _, bx1, by1, bx2, by2 = box_b

    inter_x1 = max(ax1, bx1)
    inter_y1 = max(ay1, by1)
    inter_x2 = min(ax2, bx2)
    inter_y2 = min(ay2, by1)

    inter_w = max(0, inter_x2 - inter_x1)
    inter_h = max(0, inter_y2 - inter_y1)
    intersection = inter_w * inter_h

    area_a = max(0, ax2 - ax1) * max(0, ay2 - ay1)
    area_b = max(0, bx2 - bx1) * max(0, by2 - by1)
    union = area_a + area_b - intersection

    return 0 if union == 0 else intersection / union


# (Mental model §3 → “fuse”) Recompute F[i] from L[i] by combining all evidence in the cluster
#   - “recompute F[i] from L[i]”
def fuse_cluster(cluster):
    """
    Simplified fusion:
    - fused_score: mean of scores
    - coords: weighted average by score

    (Mental model §3) This is the “fuse” step that turns one cluster (L[i]) into one fused box (F[i]).
    """
    total_score = sum(b[0] for b in cluster)
    fused_score = sum(b[0] for b in cluster) / len(cluster)

    x1 = sum(b[0] * b[1] for b in cluster) / total_score
    y1 = sum(b[0] * b[2] for b in cluster) / total_score
    x2 = sum(b[0] * b[3] for b in cluster) / total_score
    y2 = sum(b[0] * b[4] for b in cluster) / total_score

    return [fused_score, x1, y1, x2, y2]


# (Mental model §3) “For each label: sort → cluster → fuse”
#   - Inputs: B already “sorted by highest confidence first” (done in build_boxes_by_label)
#   - Maintains:
#       L = clusters (all raw boxes believed to be same object)
#       F = fused boxes (one per cluster)
#   - For each incoming box:
#       compare to fused boxes in F (IoU)
#       either create new cluster or merge & recompute fused
def weighted_box_fusion_for_label(B, iou_threshold=0.55):
    """
    Core L/F logic for a single label.
    Input B must already be sorted by score desc.  (Mental model §3: “Sort boxes …”)
    Returns:
      F: fused boxes                       (Mental model §3: F list)
      L: clusters that produced each fused box  (Mental model §3: L list)
    """
    L = []  # (Mental model §3) L: list of clusters
    F = []  # (Mental model §3) F: list of fused boxes (one per cluster)

    # (Mental model §3) Iterate “incoming boxes” in descending confidence
    for b in B:
        best_iou = 0
        best_index = -1

        # (Mental model §3) “Compare it to existing fused boxes in F”
        for idx, fused in enumerate(F):
            current = iou(b, fused)  # (Mental model §3) IoU-based “same instance?” test
            if current > best_iou:
                best_iou = current
                best_index = idx

        # (Mental model §3) “If IoU … is above a threshold → append to cluster and recompute fused”
        # else “create a new cluster and a new fused box”
        if best_iou < iou_threshold:
            L.append([b])        # (Mental model §3) create new cluster L[i]
            F.append(b)          # (Mental model §3) create new fused box F[i] (init = this box)
        else:
            L[best_index].append(b)                 # (Mental model §3) append to existing cluster
            F[best_index] = fuse_cluster(L[best_index])  # (Mental model §3) recompute fused box

    return F, L


# (Mental model §1 → §2) “Model outputs” → “Group by label (class)”
#   - Takes raw per-model detections of form [label, score, x1, y1, x2, y2] (Mental model §1)
#   - Builds {"label": [[score, x1, y1, x2, y2], ...], ...} (Mental model §2)
#   - Sorts each label’s list by score desc to satisfy Mental model §3 “Sort...” requirement
def build_boxes_by_label(*models):
    """
    models: each is a list of detections in format:
      [label, score, x1, y1, x2, y2]   (Mental model §1: model outputs)
    """
    boxes_by_label = defaultdict(list)

    # (Mental model §2) “Group by label (class)”
    for model_boxes in models:
        for label, score, x1, y1, x2, y2 in model_boxes:
            boxes_by_label[label].append([score, x1, y1, x2, y2])

    # (Mental model §3) “Sort boxes by highest confidence first”
    for label in boxes_by_label:
        boxes_by_label[label].sort(reverse=True, key=lambda b: b[0])

    return dict(boxes_by_label)


# ---- Example usage ----
# (Mental model §1) Example of raw per-model outputs: [label, score, x1, y1, x2, y2]
model_1_boxes = [
    ["cat", 0.90, 10, 10, 50, 50],
    ["dog", 0.80, 100, 100, 150, 150],
]

model_2_boxes = [
    ["cat", 0.85, 12, 11, 52, 51],
    ["dog", 0.70, 98, 99, 148, 151],
]

model_3_boxes = [
    ["cat", 0.60, 200, 200, 250, 250],
]

# (Mental model §2 + §3(sort prerequisite)) group-by-label + sort-per-label
boxes_by_label = build_boxes_by_label(model_1_boxes, model_2_boxes, model_3_boxes)

final_detections = {}
# (Mental model §3) Run “cluster → fuse” per label (never mix labels)
for label, B in boxes_by_label.items():
    fused_boxes, clusters = weighted_box_fusion_for_label(B, iou_threshold=0.55)
    final_detections[label] = fused_boxes

print(final_detections)

# (Mental model §4) Optional final confidence rescaling is not implemented in this snippet.
#   If you add it, it happens AFTER fusion, per fused box, using “num_models_contributing / num_models_total”.
```

If you want, I can also add a small “§4 rescaling” function and show exactly where it plugs in (right after `weighted_box_fusion_for_label` returns `fused_boxes`).
[Timestamp: 2026/06/02 12:54:39]

**user**: It would be better if the code is separated into code section and the comments added really make reference to the parts in the current file (in markdown/obsidian format)
[Context: Notes: Estudos/Dev/AI/Computer Vision/Post Processing/Weighted Box Fusion (WBF).md]
[Timestamp: 2026/06/02 12:55:34]

**ai**: ## Incremental code example (logic flow)

### Code

```python
from collections import defaultdict

def iou(box_a, box_b):
    _, ax1, ay1, ax2, ay2 = box_a
    _, bx1, by1, bx2, by2 = box_b

    inter_x1 = max(ax1, bx1)
    inter_y1 = max(ay1, by1)
    inter_x2 = min(ax2, bx2)
    inter_y2 = min(ay2, by1)

    inter_w = max(0, inter_x2 - inter_x1)
    inter_h = max(0, inter_y2 - inter_y1)
    intersection = inter_w * inter_h

    area_a = max(0, ax2 - ax1) * max(0, ay2 - ay1)
    area_b = max(0, bx2 - bx1) * max(0, by2 - by1)
    union = area_a + area_b - intersection

    return 0 if union == 0 else intersection / union


def fuse_cluster(cluster):
    total_score = sum(b[0] for b in cluster)
    fused_score = sum(b[0] for b in cluster) / len(cluster)

    x1 = sum(b[0] * b[1] for b in cluster) / total_score
    y1 = sum(b[0] * b[2] for b in cluster) / total_score
    x2 = sum(b[0] * b[3] for b in cluster) / total_score
    y2 = sum(b[0] * b[4] for b in cluster) / total_score

    return [fused_score, x1, y1, x2, y2]


def weighted_box_fusion_for_label(B, iou_threshold=0.55):
    L = []
    F = []

    for b in B:
        best_iou = 0
        best_index = -1

        for idx, fused in enumerate(F):
            current = iou(b, fused)
            if current > best_iou:
                best_iou = current
                best_index = idx

        if best_iou < iou_threshold:
            L.append([b])
            F.append(b)
        else:
            L[best_index].append(b)
            F[best_index] = fuse_cluster(L[best_index])

    return F, L


def build_boxes_by_label(*models):
    boxes_by_label = defaultdict(list)

    for model_boxes in models:
        for label, score, x1, y1, x2, y2 in model_boxes:
            boxes_by_label[label].append([score, x1, y1, x2, y2])

    for label in boxes_by_label:
        boxes_by_label[label].sort(reverse=True, key=lambda b: b[0])

    return dict(boxes_by_label)


# ---- Example usage ----
model_1_boxes = [
    ["cat", 0.90, 10, 10, 50, 50],
    ["dog", 0.80, 100, 100, 150, 150],
]

model_2_boxes = [
    ["cat", 0.85, 12, 11, 52, 51],
    ["dog", 0.70, 98, 99, 148, 151],
]

model_3_boxes = [
    ["cat", 0.60, 200, 200, 250, 250],
]

boxes_by_label = build_boxes_by_label(model_1_boxes, model_2_boxes, model_3_boxes)

final_detections = {}
for label, B in boxes_by_label.items():
    fused_boxes, clusters = weighted_box_fusion_for_label(B, iou_threshold=0.55)
    final_detections[label] = fused_boxes

print(final_detections)
```

---

### Mental model mapping (inline pointer references to *this section*)

Use these pointers as “anchors” you can search in this note (or convert to actual Obsidian block refs if you want).

#### [MM-1] Inputs: model outputs
- Code pointers:
  - `model_1_boxes / model_2_boxes / model_3_boxes` (the example raw detections)
  - `build_boxes_by_label(*models)` loop: `for label, score, x1, y1, x2, y2 in model_boxes:`

#### [MM-2] Group by label (class)
- Code pointers:
  - `boxes_by_label = defaultdict(list)`
  - `boxes_by_label[label].append([score, x1, y1, x2, y2])`
- Meaning:
  - Ensures fusion never mixes different classes (e.g., “cat” with “dog”).

#### [MM-3] Sort boxes by confidence (descending)
- Code pointers:
  - `boxes_by_label[label].sort(reverse=True, key=lambda b: b[0])`
- Meaning:
  - The incremental clustering logic assumes high-confidence boxes are processed first.

#### [MM-4] Per-label incremental clustering + fusion (L/F)
- Code pointers:
  - `weighted_box_fusion_for_label(B, iou_threshold=0.55)`
  - `L = []` and `F = []`
- Subparts:
  - [MM-4a] Compare incoming box to existing fused boxes
    - Code pointers:
      - `for idx, fused in enumerate(F):`
      - `current = iou(b, fused)`
  - [MM-4b] Decide: new cluster vs merge into existing
    - Code pointers:
      - `if best_iou < iou_threshold:`
      - `else:`
  - [MM-4c] Create new cluster + initialize fused box
    - Code pointers:
      - `L.append([b])`
      - `F.append(b)`
  - [MM-4d] Merge into cluster + recompute fused representative
    - Code pointers:
      - `L[best_index].append(b)`
      - `F[best_index] = fuse_cluster(L[best_index])`

#### [MM-5] Similarity metric (IoU)
- Code pointers:
  - `def iou(box_a, box_b):`
  - Called at: `current = iou(b, fused)`

#### [MM-6] Fusion rule (“recompute F[i] from L[i]”)
- Code pointers:
  - `def fuse_cluster(cluster):`
  - Called at: `F[best_index] = fuse_cluster(L[best_index])`
- Meaning:
  - Collapses a cluster of “same object” boxes into one fused box.

#### [MM-7] Output: final detections per label
- Code pointers:
  - `final_detections[label] = fused_boxes`
  - `print(final_detections)`

---

### If you want this to be *true Obsidian pointers*
If you paste this into your note, I can rewrite the code block so key lines end with block anchors like:
- `L = []  # clusters  ^mm-4-L`
Then in the mapping section we can reference them precisely:
- See `L = []  ^mm-4-L`

If you paste your current “mental model parts (and subparts)” headings exactly as they appear in the note, I can align the labels (e.g., “Part A / A.1 / A.2”) instead of using `[MM-#]`.
[Timestamp: 2026/06/02 12:55:56]

**user**: Do so
[Context: Notes: Estudos/Dev/AI/Computer Vision/Post Processing/Weighted Box Fusion (WBF).md]
[Timestamp: 2026/06/02 12:56:41]

**ai**: ## Incremental code example (logic flow)

### Code (with Obsidian block refs)

```python
from collections import defaultdict

def iou(box_a, box_b):
    # box format: [score, x1, y1, x2, y2]  ^mm-5-format
    _, ax1, ay1, ax2, ay2 = box_a
    _, bx1, by1, bx2, by2 = box_b

    inter_x1 = max(ax1, bx1)
    inter_y1 = max(ay1, by1)
    inter_x2 = min(ax2, bx2)
    inter_y2 = min(ay2, by1)

    inter_w = max(0, inter_x2 - inter_x1)
    inter_h = max(0, inter_y2 - inter_y1)
    intersection = inter_w * inter_h

    area_a = max(0, ax2 - ax1) * max(0, ay2 - ay1)
    area_b = max(0, bx2 - bx1) * max(0, by2 - by1)
    union = area_a + area_b - intersection

    return 0 if union == 0 else intersection / union  # ^mm-5-iou-return


def fuse_cluster(cluster):
    total_score = sum(b[0] for b in cluster)  # ^mm-6-total-score
    fused_score = sum(b[0] for b in cluster) / len(cluster)  # ^mm-6-fused-score

    x1 = sum(b[0] * b[1] for b in cluster) / total_score  # ^mm-6-x1
    y1 = sum(b[0] * b[2] for b in cluster) / total_score  # ^mm-6-y1
    x2 = sum(b[0] * b[3] for b in cluster) / total_score  # ^mm-6-x2
    y2 = sum(b[0] * b[4] for b in cluster) / total_score  # ^mm-6-y2

    return [fused_score, x1, y1, x2, y2]  # ^mm-6-return


def weighted_box_fusion_for_label(B, iou_threshold=0.55):
    L = []  # clusters (raw boxes grouped as same instance)  ^mm-4-L
    F = []  # fused boxes (one per cluster)                  ^mm-4-F

    for b in B:  # incoming boxes high->low confidence        ^mm-4-loop
        best_iou = 0
        best_index = -1

        for idx, fused in enumerate(F):  # compare to existing fused boxes  ^mm-4a-compare-loop
            current = iou(b, fused)  # similarity = IoU                     ^mm-4a-iou
            if current > best_iou:
                best_iou = current
                best_index = idx

        if best_iou < iou_threshold:  # new cluster vs merge decision  ^mm-4b-decision
            L.append([b])  # create new cluster                        ^mm-4c-new-L
            F.append(b)    # init fused as the first box               ^mm-4c-new-F
        else:
            L[best_index].append(b)                 # merge into cluster     ^mm-4d-merge-L
            F[best_index] = fuse_cluster(L[best_index])  # recompute fused   ^mm-4d-recompute-F

    return F, L  # ^mm-4-return


def build_boxes_by_label(*models):
    boxes_by_label = defaultdict(list)  # label -> list of boxes  ^mm-2-init

    for model_boxes in models:  # each model's outputs           ^mm-1-input-iter
        for label, score, x1, y1, x2, y2 in model_boxes:  # raw detection tuple  ^mm-1-raw-format
            boxes_by_label[label].append([score, x1, y1, x2, y2])  # group by label  ^mm-2-append

    for label in boxes_by_label:
        boxes_by_label[label].sort(reverse=True, key=lambda b: b[0])  # sort by confidence desc  ^mm-3-sort

    return dict(boxes_by_label)  # ^mm-2-return


# ---- Example usage ----
model_1_boxes = [  # raw model outputs  ^mm-1-example-1
    ["cat", 0.90, 10, 10, 50, 50],
    ["dog", 0.80, 100, 100, 150, 150],
]

model_2_boxes = [  # raw model outputs  ^mm-1-example-2
    ["cat", 0.85, 12, 11, 52, 51],
    ["dog", 0.70, 98, 99, 148, 151],
]

model_3_boxes = [  # raw model outputs  ^mm-1-example-3
    ["cat", 0.60, 200, 200, 250, 250],
]

boxes_by_label = build_boxes_by_label(model_1_boxes, model_2_boxes, model_3_boxes)  # group+sort  ^mm-2-3-call

final_detections = {}  # label -> fused detections  ^mm-7-init
for label, B in boxes_by_label.items():  # per-label fusion (never mix labels)  ^mm-7-per-label
    fused_boxes, clusters = weighted_box_fusion_for_label(B, iou_threshold=0.55)  # cluster+fuse  ^mm-7-fuse-call
    final_detections[label] = fused_boxes  # output per label  ^mm-7-assign

print(final_detections)  # ^mm-7-print
```

---

### Mental model mapping (with direct block references)

- **[MM-1] Inputs: model outputs**
  - Format: see `box format` in [[#^mm-5-format]] and raw tuple in [[#^mm-1-raw-format]]
  - Examples: [[#^mm-1-example-1]], [[#^mm-1-example-2]], [[#^mm-1-example-3]]

- **[MM-2] Group by label (class)**
  - Initialize label buckets: [[#^mm-2-init]]
  - Append to label group: [[#^mm-2-append]]
  - Return grouped mapping: [[#^mm-2-return]]

- **[MM-3] Sort boxes by confidence**
  - Per-label sort: [[#^mm-3-sort]]

- **[MM-4] Per-label incremental clustering + fusion (L/F)**
  - Cluster list $L$: [[#^mm-4-L]]
  - Fused list $F$: [[#^mm-4-F]]
  - Incoming loop: [[#^mm-4-loop]]
  - Return $(F, L)$: [[#^mm-4-return]]

  - **[MM-4a] Compare incoming box to existing fused boxes**
    - Iterate fused candidates: [[#^mm-4a-compare-loop]]
    - IoU computation call: [[#^mm-4a-iou]]

  - **[MM-4b] Decide: new cluster vs merge**
    - Threshold decision point: [[#^mm-4b-decision]]

  - **[MM-4c] Create new cluster + initialize fused**
    - New $L[i]$: [[#^mm-4c-new-L]]
    - New $F[i]$: [[#^mm-4c-new-F]]

  - **[MM-4d] Merge into cluster + recompute fused**
    - Merge into $L[i]$: [[#^mm-4d-merge-L]]
    - Recompute $F[i]$ from $L[i]$: [[#^mm-4d-recompute-F]]

- **[MM-5] Similarity metric (IoU)**
  - IoU return value: [[#^mm-5-iou-return]]

- **[MM-6] Fusion rule (“recompute $F[i]$ from $L[i]$”)**
  - Total score: [[#^mm-6-total-score]]
  - Fused score: [[#^mm-6-fused-score]]
  - Weighted coordinates: [[#^mm-6-x1]], [[#^mm-6-y1]], [[#^mm-6-x2]], [[#^mm-6-y2]]
  - Return fused box: [[#^mm-6-return]]

- **[MM-7] Output assembly (per label)**
  - Create output dict: [[#^mm-7-init]]
  - Per-label processing: [[#^mm-7-per-label]]
  - Run fusion: [[#^mm-7-fuse-call]]
  - Assign output: [[#^mm-7-assign]]
  - Print: [[#^mm-7-print]]

If your “mental model parts” in the note use specific headings (e.g., “Part 1: Normalize → 1.1 …”), paste those headings and I’ll rename `[MM-*]` to match them exactly while keeping the same block references.
[Timestamp: 2026/06/02 12:57:02]