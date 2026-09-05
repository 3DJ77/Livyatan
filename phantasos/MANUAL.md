# Phantasos — Operator Manual

Sovereign AI image generation. Type a prompt, get a 1024² render on canvas.
A module of the Livyatan Design Suite; licensed PolyForm Small Business.

## Quickstart

```
sudo apt install ./phantasos_<version>_amd64.deb
phantasos
```

1. Window opens. Nothing renders until stable-diffusion.cpp and weights are
   in place — see the README for setup.
2. Type a prompt in the text box. Press **Shape** (the button — Enter commits
   the text but does not render).
3. Status reads `shaping with <model>…`. First render pays the model load;
   after that, renders stay fast until you switch models.
4. The render fills the **canvas** and joins the **folio** strip on the right.
5. **Open in gimp** (or whatever's current) hands the full-res PNG to an editor;
   **swap** cycles to the next installed editor. **Fit to monitor** opens a
   monitor-sized copy.

Everything runs on the machine Phantasos is launched on — no network, no
remote host.

## What it is

A standalone Rust app (fyrox window + the `image` crate, Kish-style). It is
the image half of "image + report": **Phantasos** makes the picture, **Kish**
makes the report. It made every Livyatan module splash and the LIVYATAN
masthead.

No web tech. No Python UI. One binary, one window, your own GPU.

## Why the name

Phantasos is one of the Oneiroi, brother of Morpheus — the dream-spirit
whose specific gift was dreams of *inanimate objects*: stone, wood, water,
the shapes of things. This module dreams pictures of objects so the rest of
the suite can make them real. Kin in the pantheon:

- **Galatea** — reserved for the video layer (still → motion), later.

## Features

- **Canvas + folio** — big canvas shows the latest render; every render joins
  the folio (thumbnail strip, newest on top). Click a thumbnail to bring it back.
- **Model picker** — `Model:` button cycles the three offered models, persisted
  to `~/.config/phantasos/model`:
  - **Klein** (FLUX.2 klein 4B, Apache-2.0) — 4 steps, cfg 1.0, euler. Resident.
    Default. With a start image it **edits** (reference lane: the image rides
    along as context, the prompt is the change) — no strength knob.
  - **Schnell** (FLUX.1 Schnell, Apache-2.0) — 4 steps, cfg 1.0, euler. Resident.
  - **FLUX.2 dev** — 20 steps. Non-resident, one-shot (slow by design).
- **Fetch** — pulls the selected model's weights from the publisher into
  `PHANTASOS_MODEL_DIR` (same table as `phantasos fetch MODEL`; `phantasos
  models` lists what's installed). Resumable, size-verified, one file at a
  time, progress in the status line. Shape on an unfetched model fails loud
  with the command to run.
- **Two execution paths** — the resident model POSTs the **A1111 API**
  (`http://127.0.0.1:<port>/sdapi/v1/txt2img`) to a local `sd-server`
  Phantasos starts and keeps warm (no per-render reload; the model loads
  lazily on the first render).
  The non-resident model runs one-shot via a local `sd-cli` call.
- **Open in…** — hands the current render to gimp/krita/inkscape/gthumb/eog/
  feh/nomacs; first installed wins, `swap` cycles, choice persisted to
  `~/.config/phantasos/editor`.
- **Fit to monitor** — native Lanczos resize to the monitor the window is
  on (up or down), then opens the copy in the editor.

| var | default | what |
|---|---|---|
| `PHANTASOS_MODEL_DIR` | `~/.local/share/phantasos/models` | weight files (`flux2-klein/`, `flux/`, `flux2/`) |
| `PHANTASOS_SD_DIR` | (PATH) | directory holding `sd-server`/`sd-cli` |
| `PHANTASOS_SD_PORT` | `7860` | local A1111 port `sd-server` listens on |
| `PHANTASOS_OUT_DIR` | `~/Phantasos` | where renders land |
| `PHANTASOS_STRENGTH` | `0.6` | img2img denoise for `--from` on Schnell / FLUX.2 dev (0.0 exclusive to 1.0; klein's reference lane ignores it) |

Model file paths and per-model flags live in `model_args()` in `src/main.rs` —
the single source of recipe truth for both execution paths.

The weight files each model pulls, their sizes and their publishers are
tabulated in the README; they live under `PHANTASOS_MODEL_DIR` in
`flux2-klein/`, `flux/` and `flux2/`.

## Headless

```
phantasos shape "PROMPT" [OUT.png] [--model NAME] [--seed N] [--size PX] [--from IMAGE]
```

Same pipeline as the window, same recipe table, prints the output path.

- `--model NAME` — `klein`, `schnell` or `flux2dev` (display names work too).
  Defaults to klein, not to the window's persisted pick. An unknown name
  lists the valid ones and exits 1.
- `--seed N` — integer seed; default `-1`, which is random. This is the only
  way to get a reproducible render — the window has no seed field.
- `--size PX` — the square output edge, used for both width and height.
  Default 1024, accepted range 256 to 4096; anything outside that exits 1.
  It reaches both execution paths (`width`/`height` in the A1111 payload,
  `-W`/`-H` on `sd-cli`). CLI only — the window is fixed at 1024². The models
  are trained at 1024, so off-1024 sizes are a knob, not a free win: smaller
  renders faster and lighter, larger will blow past an 8 GB card.
- `--from IMAGE` — start image. On klein it is a reference (composition
  stays, the prompt is the change); on Schnell and FLUX.2 dev it is img2img
  at `PHANTASOS_STRENGTH`. A path that isn't a file exits 1.

## Using it

- **Render**: pick a model, type, Shape. Status line tells you what's happening;
  there's no progress bar yet — "shaping…" then the image lands.
- **Cold start**: first render after Phantasos starts or a model switch blocks
  while it loads the model (idempotent — a no-op if that model is already
  resident, otherwise it kills the old server, starts the new one, and waits
  for "listening on" or fails loud).
- **Model switch**: cycling the Model button is free; the load cost is paid on
  the next Shape.
- **Revisit**: click any folio thumbnail — canvas swaps back, Open/Fit act on it.
- **Files**: everything is a plain PNG in `PHANTASOS_OUT_DIR` (default
  `~/Phantasos`).

## How it connects

```
Phantasos (this machine, this window)
  ├─ ensure_server(key)               make the model resident (no-op if warm)
  │     └─ sd-server                  local process, one model resident
  ├─ curl 127.0.0.1:<port>            A1111 txt2img, local loopback only
  └─ ~/Phantasos/*.png                 render lands on local disk
```

Everything is local — no network calls, no remote host, no shared lease
file. If something else on the machine is also hammering the GPU at the
same time, that's between you and your driver; Phantasos makes no claim on
it beyond its own render.

Siblings: **Kish** (reports) is the text half of the release pipeline;
**Galatea** (video) is reserved.

## Known limits

- **Fixed steps; size is CLI-only** — `phantasos shape --size PX` takes
  256..4096 (square), but the window still renders 1024² and step counts are
  fixed per model. Steps control and a size row in the window are the next
  small add.
- **FLUX.2 dev is slow one-shot by design** — its long `--offload-to-cpu`
  first step outlasts a kept-open server connection, so it can't ride the
  resident path.
- **Cold-start tax** — first render after Phantasos starts or a model switch
  pays the full model load from disk. Not persisted across a Phantasos
  restart — every fresh launch reloads on first render.
- **No negative prompt, no seed control** — seed is `-1` (random) today.
- **No progress bar** — status text only.
- **Chroma1-HD and FLUX.1 dev aren't offered** — both weave a cross-hatch
  artifact on constrained-VRAM Vulkan paths across every knob tried. Do not
  re-wire without an upstream fix.

## Queued

- Steps control and a size row in the prompt row (`--size` exists headless).
- Seed field for reproducibility; negative prompt.
- Progress feedback during long shapes.
- **Galatea** — sd-cli has `-M vid_gen`; the still→motion layer.
