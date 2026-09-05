# Phantasos

**AI image generation, fully local. Type a prompt, get a render — on
whatever GPU you have.** This is the **klein fork**: FLUX.2 klein 4B is
the default model, and "start from an image" is a real edit (the picture
is a reference, the prompt is the change) instead of a redraw.

## Hardware

**Tier 2 — needs a real GPU.** Backend is
[stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp)'s
Vulkan build, so it runs on any GPU that backend supports (AMD, Intel,
NVIDIA) — not tied to one vendor or one machine. Everything runs on the
box Phantasos is launched on: no network, no remote host, no account.

Klein (FLUX.2 klein 4B, Q8) is **unmeasured on the ladder** so far — the
weights are 4.3 GB plus an 8 GB Qwen3-4B text encoder that runs on the
CPU, so it is expected to fit an 8 GB card like Schnell does, but expected
is not measured; the numbers land here when they exist.

Measured floor (NVIDIA T1000 8GB, FLUX.1 Schnell q4, 1024x1024, 4 steps):
first render ~6.5 min including model load, ~5 min per render after —
sampling is ~4.5 min of that. The card must be otherwise free: the
diffusion weights alone are 6.9GB, so 8GB is the working minimum and
anything else resident on the GPU (a model server, a game) will starve it.
Text encoding runs on the CPU and VAE decode is tiled by default, which is
what makes 8GB cards work at all; bigger cards pay a few seconds for the
same defaults. FLUX.2 dev wants more headroom and patience — it renders
one-shot with CPU offload and takes minutes even on large cards.

## Why this exists

The author wanted alternatives to paid services and subscription programs.
Same capability — type a prompt, get an image — running entirely on your
own machine.

## Quickstart

1. **Build stable-diffusion.cpp** (Vulkan backend) and put `sd-server` and
   `sd-cli` on your `PATH`, or set `PHANTASOS_SD_DIR` to the directory
   holding them. You also need a working **Vulkan driver** (loader + your
   GPU's ICD — `mesa-vulkan-drivers` covers AMD/Intel on Debian) and
   **`curl`** (the render path POSTs to the local server with it; the deb
   depends on it).
2. **Get weights.** Nothing ships in the deb (the sets are 12–68 GB).
   Pick a model and let Phantasos pull it from the publisher:

   ```bash
   phantasos models          # what's offered, size, installed or not
   phantasos fetch klein     # FLUX.2 klein 4B — the default, ~12.7 GB
   phantasos fetch schnell   # FLUX.1 Schnell, ~17 GB (optional)
   phantasos fetch flux2dev  # FLUX.2 dev, ~42 GB (optional, non-commercial)
   ```

   Or press **Fetch** in the window next to the model picker — it pulls
   whichever model is selected and narrates in the status line. Downloads
   are resumable (a `.part` file stays put on failure) and verified by size.
   Weights land in `PHANTASOS_MODEL_DIR` (default
   `~/.local/share/phantasos/models`, under `flux2-klein/`, `flux/`,
   `flux2/`); point that at an existing directory if you already have them.
   Model weights are licensed by their publishers, not by this tool
   (FLUX.2 klein and FLUX.1 Schnell are Apache-2.0; FLUX.2 dev carries
   Black Forest Labs' non-commercial license).

### Weight files

`phantasos fetch` writes into `PHANTASOS_MODEL_DIR` (default
`~/.local/share/phantasos/models`) under one subdirectory per model family.
Sizes are the publisher's exact byte counts — the fetch verifies them, so a
truncated download never masquerades as installed.

| model | file | size | from |
|---|---|---|---|
| klein | `flux2-klein/flux-2-klein-4b-Q8_0.gguf` | 4.3 GB | `leejet/FLUX.2-klein-4B-GGUF` |
| klein | `flux2-klein/qwen_3_4b.safetensors` | 8.0 GB | `Comfy-Org/flux2-klein-4B` |
| klein, flux2dev | `flux2/flux2-vae.safetensors` | 0.34 GB | `Comfy-Org/flux2-klein-4B` |
| schnell | `flux/flux1-schnell-q4_0.gguf` | 6.9 GB | `leejet/FLUX.1-schnell-gguf` |
| schnell | `flux/t5xxl_fp16.safetensors` | 9.8 GB | `comfyanonymous/flux_text_encoders` |
| schnell | `flux/clip_l.safetensors` | 0.25 GB | `comfyanonymous/flux_text_encoders` |
| schnell | `flux/ae.safetensors` | 0.34 GB | `black-forest-labs/FLUX.1-schnell` |
| flux2dev | `flux2/flux2-dev-Q6_K.gguf` | 27.4 GB | `city96/FLUX.2-dev-gguf` |
| flux2dev | `flux2/Mistral-Small-3.2-24B-Instruct-2506-Q4_K_M.gguf` | 14.3 GB | `unsloth/Mistral-Small-3.2-24B-Instruct-2506-GGUF` |

All are `https://huggingface.co/<repo>/resolve/main/<file>`. Klein's VAE sits
under `flux2/`, not `flux2-klein/` — FLUX.2 dev uses the same file, and it is
only fetched once. If you already have these files, point
`PHANTASOS_MODEL_DIR` at the directory that holds those three subdirectories
rather than downloading them again.

3. **Run `phantasos`.** Type a prompt, press Shape. First render pays the
   model load; after that it's resident and stays fast. Switch models any
   time with the **Model** button (or `--model` on the CLI) — a model you
   haven't fetched fails loud with the fetch command, never a hang.

Headless, same pipeline (prints the output path; `--seed` makes it
reproducible):

```bash
phantasos shape "a lighthouse at dusk" out.png
phantasos shape "a lighthouse at dusk" out.png --model schnell --seed 42
phantasos shape "make the lamp brass" out.png --from lighthouse.png
phantasos shape "a lighthouse at dusk" out.png --size 768
```

`--size PX` sets the square output edge — width and height both — default
1024, accepted range 256 to 4096. It is a CLI-only flag; the window always
renders 1024x1024. Off-1024 sizes are unmeasured and the models are trained
at 1024, so expect quality and VRAM behaviour to move with it: smaller is
faster and lighter, larger will exceed an 8 GB card.

With `--from` on Klein the image is a **reference**: composition stays,
the prompt says what changes. On Schnell / FLUX.2 dev the same flag is
img2img (redraw at `PHANTASOS_STRENGTH`, default 0.6).

Other suite modules use this seam too: GilgaMESH's words mode and Kish's
folio plates render through `phantasos shape` when it's on your PATH.

## Models

- **Klein** (default) — FLUX.2 klein 4B, 4 steps, resident. Text-to-image
  and reference edit in one model.
- **Schnell** — 4 steps, fast, resident (stays loaded between renders).
- **FLUX.2 dev** — slower, higher quality, one-shot (its CPU-offload first
  step outlasts a kept-open server connection, so it renders standalone
  each time).

Chroma1-HD and FLUX.1 dev aren't offered — both produce a visible weave
artifact on constrained-VRAM Vulkan paths across every setting tried.

## Known limitations

- Fixed step counts per model. Output is fixed 1024² in the window;
  headless, `phantasos shape --size PX` takes 256..4096 (square only).
- No negative prompt; no seed field in the window — window renders are
  random-seed (headless `phantasos shape --seed` is reproducible).
- No progress bar — status text only ("shaping…" then the image lands).
- First render after a fresh start or a model switch pays the full model
  load; after that, renders stay fast until you switch models again.

## Credits

- [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp) —
  the local inference engine.
- [FLUX.2 klein / FLUX.1 Schnell / FLUX.2 dev](https://huggingface.co/black-forest-labs) —
  Black Forest Labs; klein and Schnell Apache-2.0, dev non-commercial.

[PolyForm Small Business 1.0.0](LICENSE.md) — free for individuals and
small shops.

If this saved you a subscription and you've got a few spare bucks:
[ko-fi.com/3DJ77](https://ko-fi.com/3DJ77). Appreciated, never required.
