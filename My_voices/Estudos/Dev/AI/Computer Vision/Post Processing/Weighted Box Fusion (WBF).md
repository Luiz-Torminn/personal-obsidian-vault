---
type: method
tags: [ai, computer-vision, post-processing, object-detection, weighted-box-fusion, wbf]
---
# Weighted Box Fusion (WBF)

- **Does not discard** bounding boxes; it **combines** them to use information from *all* models.
- Contrast: **NMS** removes (“suppresses”) overlapping boxes, potentially discarding useful evidence.

## Mental model (per image / frame)

### 1) Model outputs
Each detection model returns boxes in the form:

`[label, score, x1, y1, x2, y2]`

Example:

- `model_1 = [[label, score, x1, y1, x2, y2], ...]`

### 2) Group by label (class)
WBF fuses **only within the same label** (e.g., “cat” with “cat”, never “cat” with “dog”).

You can build a dictionary like:

- `{"label_1": [[score, x1, y1, x2, y2], ...], "label_2": [...], ...}`

### 3) For each label: sort → cluster → fuse
For each label’s list of boxes:

- Sort boxes by **highest confidence first**.
- Identify which boxes refer to the **same object instance** (same label, same location) using **IoU**.
- Maintain:
  - `L`: list of **clusters** (each cluster = boxes believed to be the same object)
  - `F`: list of **fused boxes** (one fused box per cluster)

**How clustering works (L ↔ F relationship):**
- Each cluster in `L` corresponds to exactly one fused box in `F`.
- For each incoming box:
  - Compare it to existing fused boxes in `F`.
  - If IoU with some `F[i]` is above a threshold:
    - append the box to cluster `L[i]`
    - recompute `F[i]` from `L[i]`
  - Otherwise:
    - create a new cluster in `L`
    - create a new fused box in `F` (initially equal to that box)

### 4) Final confidence rescaling (optional but common)
After fusion, rescale each fused confidence based on how many **models** agreed:

`final_score = fused_score * (num_models_contributing / num_models_total)`

> [!NOTE]
> If you use `number_of_boxes_in_cluster` directly, a single model producing duplicates can inflate confidence. Prefer counting **unique contributing models** per cluster when possible.
> 
> For this, you can use [[Non-Maximum Suppression (NMS)]] to avoid a single model making multiple predictions for the same element.

---

## Incremental code example (logic flow)

```python
from collections import defaultdict

def iou(box_a, box_b):
    # box format: [score, x1, y1, x2, y2]
    _, ax1, ay1, ax2, ay2 = box_a
    _, bx1, by1, bx2, by2 = box_b

    inter_x1 = max(ax1, bx1)
    inter_y1 = max(ay1, by1)
    inter_x2 = min(ax2, bx2)
    inter_y2 = min(ay2, by2)

    inter_w = max(0, inter_x2 - inter_x1)
    inter_h = max(0, inter_y2 - inter_y1)
    intersection = inter_w * inter_h

    area_a = max(0, ax2 - ax1) * max(0, ay2 - ay1)
    area_b = max(0, bx2 - bx1) * max(0, by2 - by1)
    union = area_a + area_b - intersection

    return 0 if union == 0 else intersection / union


def fuse_cluster(cluster):
    """
    Simplified fusion:
    - fused_score: mean of scores
    - coords: weighted average by score
    """
    total_score = sum(b[0] for b in cluster)
    fused_score = sum(b[0] for b in cluster) / len(cluster)

    x1 = sum(b[0] * b[1] for b in cluster) / total_score
    y1 = sum(b[0] * b[2] for b in cluster) / total_score
    x2 = sum(b[0] * b[3] for b in cluster) / total_score
    y2 = sum(b[0] * b[4] for b in cluster) / total_score

    return [fused_score, x1, y1, x2, y2]


def weighted_box_fusion_for_label(B, iou_threshold=0.55):
    """
    Core L/F logic for a single label.
    Input B must already be sorted by score desc.
    Returns:
      F: fused boxes
      L: clusters that produced each fused box
    """
    L = []  # clusters
    F = []  # fused boxes (one per cluster)

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
    """
    models: each is a list of detections in format:
      [label, score, x1, y1, x2, y2]
    """
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