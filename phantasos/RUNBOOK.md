# Phantasos — Runbook

*Prompt → image. Tier 2 — needs a real GPU (8 GB VRAM working minimum;
built and tested on an NVIDIA T1000 8 GB, where a first render is ~6.5
minutes and later renders ~5). Backend is stable-diffusion.cpp (Vulkan).*

## Install and launch

```
sudo apt install ./phantasos_<version>_amd64.deb
phantasos
```

Setup (one time): build stable-diffusion.cpp, install a Vulkan driver, then
`phantasos fetch klein` (~12.7 GB, the default model; `phantasos models`
lists the others) — the README walks all three.

## The five-minute tour

- Type a prompt, press **Shape**. The status line narrates: first render
  loads the model (minutes — the wait is the load, not a hang), then the
  model stays resident and renders come faster.
- The render fills the canvas and joins the folio strip on the right;
  click a thumbnail to bring one back.
- **Open in gimp** hands the full-res PNG to an editor; **swap** cycles
  editors. Renders land in `~/Pictures` by default; **Folder…** on the bar picks another
  (remembered in `~/.config/phantasos/out_dir`); `PHANTASOS_OUT_DIR` overrides both.
- Closing the window shuts the resident server down and frees the GPU.

## Worked example — and the chain

Shape this:

```
a cast-iron wall bracket, scrolled acanthus leaves, straight on,
plain white background
```

Open the result once to check the silhouette reads clean. That PNG is
the chain link: feed it to **GilgaMESH** (`gilgamesh chain bracket.png`
or the Pick image… button) and it comes back a watertight STL; scale
and cut it in **Structor** / **Hephaestus** from there. Phantasos makes
the picture; the rest of the suite makes it matter.

Headless, same pipeline:

```
phantasos shape "a cast-iron wall bracket ..." --seed 7 --size 1024
```

prints the output path — scriptable from anything. `--seed` makes it
reproducible, `--size PX` sets the square edge (256..4096, default 1024,
CLI only), `--model NAME` picks klein/schnell/flux2dev and `--from IMAGE`
starts from a picture you already have.

## The window

Top bar, one button high, in three panes across the window (Structor's layout): FILE
(Folder…, Save as…, Export…, Pick image…, Open in gimp, swap), BUILD (Create Image, Model,
Fetch), NAV/UI (Weights…, Server, Fit, A+/A-). The weights folder in force
shows in the status line. While a model loads or a render runs, the picture area shows a blown-glass hourglass
with real falling sand: a cellular automaton (each grain falls, slides or rolls; the crater,
the stream and the heap follow), paced so the top empties in the time the last render of
that model on that server took (`~/.config/phantasos/timing.json`, learned per run) or, for
a fetch, by its reported bytes. Past the expected time the glass turns over and drains again.

## Knobs

Weights live in the folder on the **Weights:** button. On first run Phantasos looks
for a store that already holds a known weight file — `~/models/image` or
`<any mount>/models/image` — and remembers it; otherwise the default is
`~/.local/share/phantasos/models`. If no model is installed anywhere it looked, the
first launch asks which models to download (Klein ticked) and fetches them with the
same progress line as the Fetch button; Cancel leaves it to the Fetch button. Pick
another folder on the Weights button, or set `PHANTASOS_MODEL_DIR` to override — the README tables every file and its
size. **Server:** renders load the model on this machine unless the Server button
names a running sd-server (`host:port`, e.g. a GPU box on the LAN started with
`sd-server … --listen-ip 0.0.0.0`); then nothing loads here, no local weights are
needed, and that server renders with whatever model it has loaded.
`PHANTASOS_SD_SERVER` overrides the button. `PHANTASOS_SD_DIR` points at `sd-server`/`sd-cli` when they are not on
PATH, `PHANTASOS_SD_PORT` (default 7860) is the loopback port the resident
server listens on, and `PHANTASOS_STRENGTH` (default 0.6) is the img2img
denoise for `--from` on Schnell and FLUX.2 dev.
