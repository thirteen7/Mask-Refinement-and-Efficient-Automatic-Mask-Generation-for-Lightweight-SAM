# Curated point and box comparisons

Point and Box use four annotated COCO examples with fixed foreground prompts.
**Run both models** compares the original and refined outputs for the initial
prompt. **+1 point** and **+2 points** add the preset corrections one at a time.
Two panels show the current stage; the IoU table tracks completed stages.
Use **Everything** to upload an image for automatic mask generation.

## Original model policy

Both paths use the same frozen base in the released complete checkpoint.
TinySAM chooses the highest native predicted-IoU score among its three public
candidates. MobileSAM uses three public candidates for the initial point and
the native single-mask output for boxes and later point stages. The original
path calls the native decoder. Each method retains its own selected previous
logits, and both receive identical prompts. Native scores select the original
candidate; ground-truth IoU measures the result.

## True IoU and recorded assets

The gallery carries the legacy target mask: nearest resize to a longest side
of 1024, followed by bilinear restoration and the positive threshold used by
the interaction evaluation. Live IoU is recomputed from each prediction's
integer intersection and union with that mask. It is distinct from SAM's
predicted-IoU score. The gallery uses the original photographs.

[examples.json](../site/examples.json) records the image, annotation, checkpoint
fingerprints, foreground coordinates, GT file, mask fingerprints and exact
intersection/union counts. The static explorer uses recorded CPU predictions;
the studio runs the selected checkpoint on the current device.

| Backbone | Prompt | COCO image | Target |
|---|---|---:|---|
| TinySAM | Point | 110972 | Black bear |
| TinySAM | Box | 414795 | Elephant |
| MobileSAM | Point | 79651 | Bottle |
| MobileSAM | Box | 329080 | Bed |

## Gallery and dataset protocols

The gallery selects CC BY photographs and foreground coordinates that show
initial and corrected outputs clearly. Annotations guide click placement and
per-image scoring. In the [dataset evaluation](results.md), each method
generates its own correction trajectory using foreground or background clicks.

Everything uses the separate frozen ViT-H FSD pathway. Its animation explains
the flow; paired mask views and milliseconds come from actual inference.
