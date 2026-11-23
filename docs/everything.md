# Everything mode

Everything generates instance masks from an automatically sampled point grid.
Each run uses a frozen SAM backbone and its three public mask candidates.
Overlay colors identify individual instances.

## Run

```bash
python download_models.py --model tinysam
python generate.py --checkpoint weights/tinysam_prompt_adaptive_v1.pth \
  --image example.jpg --method fsd --grid 32 --output runs/everything
```

Use `--device cuda` for a compatible CUDA installation. Choose `--method dense`
for native dense SAM decoding. The Python interface is:

```python
from prompt_adaptive_sam import Predictor, EverythingGenerator

p = Predictor('weights/tinysam_prompt_adaptive_v1.pth', device='cuda')
masks, details = EverythingGenerator(p, method='fsd', points_per_side=32).generate(rgb)
```

Each output includes a COCO-format RLE mask, pixel area, bounding box, the native
SAM predicted IoU, and stability score.

## Inference paths

**FSD-SAM** computes complete independent prompt factors, native phase-(0,0)
previews, four-wave selection, and local small-region protection. Retained
requests complete native suffix decoding. The hosted application runs the
portable PyTorch decoder, and the [COCO100 benchmark](results.md#segment-everything-timing)
reports the fused CUDA implementation. Preview and local checks estimate which
prompts to complete.

**Dense SAM** completes each sampled request through the native decoder.
Both paths use fixed predicted-IoU 0.88, stability 0.95, NMS 0.7, three public
mask candidates, and no image crops. The grid is 8×8, 16×16, or 32×32.
The live studio and CLI default to 32×32. The recorded project-page comparison
uses 16×16.

## Website and application

The GitHub Pages explorer displays a recorded paired ViT-H comparison. Press
**Show recorded comparison** to reveal Dense SAM on the left and FSD-SAM on
the right, with measured milliseconds and completed-request counts. Both use
the same frozen ViT-H weights, image, 16×16 grid and filters. The standalone
process animation shows encoding, prompt factors, previews, suffix completion
and filtering, with replay, pause and manual step controls.

In the hosted/local studio, **Run both models** runs both paths on the current
image and shows their masks and times together. Each synchronized total is the
shared image-encoding time plus that method's mask-generation time. The studio
warms both methods before timing and alternates their order on repeated runs.
The **How FSD works** animation receives actual FSD request/mask counts.

The instance inspector shows the native SAM predicted IoU for each generated
mask. Open **Paper results** for the aggregate COCO100 timing and quality metrics.
