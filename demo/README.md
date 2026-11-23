# Research studio

The same Gradio studio is used locally and in the Hugging Face Space.

## Run locally

Install the project and `demo/requirements.txt`, then run:

```bash
SAM_DEMO_DEVICE=cpu python demo/space/app.py
```

Windows PowerShell:

```powershell
$env:SAM_DEMO_DEVICE='cuda'  # use cpu without CUDA
python demo/space/app.py
```

The launcher detects the local checkout. Open `http://127.0.0.1:7860`.
The launcher downloads missing checkpoints and verifies their SHA256 hashes.
The default CUDA path uses the local device for a local checkout, and ZeroGPU
in a hosted Space.

## Compare lightweight models

Point and Box offer four annotated examples: black bear, elephant, bottle and
bed. Choose a thumbnail and press **Run both models** for the initial prompt.
Use **+1 point** and **+2 points** in order to add the preset foreground
corrections. **Previous result / Next result** recalls saved images, prompts,
and target IoU. Corrections continue from the latest completed stage.

Both paths receive the same prompts and keep their own previous logits in CPU
session memory. The studio scores each stage against the legacy target mask.
See the [gallery and dataset protocols](../docs/showcase.md).

## Compare automatic generation

Everything accepts image uploads or built-in examples. One button compares
SAM ViT-H / Dense on the left and FSD-SAM / ViT-H on the right. Both paths use
the same grid, frozen base and filters. The default grid is 32 × 32 (1,024
independent foreground prompts). CUDA-synchronized totals include shared image
encoding plus each generation time. Repeat runs alternate execution order.
The instance inspector reports SAM's predicted IoU. **Paper results** lists
the COCO100 benchmark for TinySAM, MobileSAM and SAM ViT-H.
The FSD animation maps every prompt onto the image and shows the actual four
selection waves and local-guard additions. Click a point to inspect its pixel
coordinates and selection reason; playback and step controls explain the order.

## Hugging Face deployment

Upload `app.py`, `README.md` and `requirements.txt` from `demo/space/` to the
existing Gradio Space after the corresponding project code is published.
The hosted launcher clones the public project into its versioned cache.
Select ZeroGPU hardware. The comparison callback requests the GPU for inference.

Gradio uses temporary storage for uploads and rendered outputs, cleaned on
a 15-minute schedule. Image state and measured masks stay in CPU session memory;
each paired run uses independent logits internally.
Use `demo/server.py` for local API development and `demo/space/app.py` for
the Gradio studio.
