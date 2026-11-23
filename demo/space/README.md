---
title: Mask Refinement and Efficient Automatic Mask Generation for Lightweight SAM
emoji: 🔬
colorFrom: purple
colorTo: blue
sdk: gradio
sdk_version: 5.49.1
python_version: '3.10'
app_file: app.py
pinned: false
license: other
---

# Mask Refinement and Efficient Automatic Mask Generation for Lightweight SAM

[Project page](https://thirteen7.github.io/Mask-Refinement-and-Efficient-Automatic-Mask-Generation-for-Lightweight-SAM/) ·
[Code and models](https://github.com/thirteen7/Mask-Refinement-and-Efficient-Automatic-Mask-Generation-for-Lightweight-SAM)

**Point & Box:** Compare original and refined TinySAM or MobileSAM on four
annotated examples. Run the initial prompt, then add **+1 point** and **+2 points**
in order. Each stage shows both masks and target IoU. [Comparison protocol](https://github.com/thirteen7/Mask-Refinement-and-Efficient-Automatic-Mask-Generation-for-Lightweight-SAM/blob/main/docs/showcase.md).

**Everything:** Upload an image or choose an example, then press **Run both models**.
The studio compares Dense and FSD-SAM on the same frozen SAM ViT-H, with shared
input, grid and native filters. Inspect the masks, predicted IoU and measured
encoding-plus-generation times. The portable PyTorch demo runs on ZeroGPU and
stores uploads and predictions in a temporary cache.

**How FSD works:** Play or step through the grid, selection waves and mask completion.

**Paper results:** Compare Dense, Hierarchical and FSD-SAM on COCO100 for
TinySAM, MobileSAM and SAM ViT-H. [View the benchmark on the project page](https://thirteen7.github.io/Mask-Refinement-and-Efficient-Automatic-Mask-Generation-for-Lightweight-SAM/#fsd-results).

License: see the project's LICENSE and NOTICE.
