# GilgaMESH

**Photo or prompt → watertight, correctly-oriented, mm-scaled STL. Fully
local, AMD/Vulkan friendly, no cloud, no subscription, no account.**

The missing last mile for [trellis.cpp](https://github.com/pwilkin/trellis.cpp):
every image-to-3D project stops at "here's a GLB for your renderer." This one
ends where your slicer begins.

*Paper, rock, scissors — the photo is the paper, the mesh is the rock,
your slicer is the scissors. Paper becomes rock, rock goes to the
scissors. A new way to play an old game.*

## Hardware

Measured on real machines, one photo of a Benchy through the whole chain
(reconstruction quality varies run to run; times are one honest sample,
not a benchmark):

| your hardware | what works | measured |
|---|---|---|
| big unified memory (AMD Strix Halo, 128 GB) | **full chain**: photo → textured GLB + sliceable STL | ~24 min end-to-end |
| 8 GB GPU + desktop CPU (tested: 8 GB workstation card, 20 cores) | **light chain** (geometry-only trellis, `--no-texture --res 512`): photo → sliceable STL | ~10 min end-to-end, 4 GB RAM |
| 4 GB GPU laptop (tested: GTX 1650, 12 cores) | **repair only** — generation weights don't fit 4 GB | `gilgamesh remesh` on a 296k-face mesh: 36 s, 1.4 GB RAM |
| any CPU, no GPU | **repair only** | scales with cores |

Two honest notes: the full-resolution reconstruction is also the *cleaner*
one (our full-mode run shed 20 debris bodies; the light-mode run shed
4,411 — texture mode hallucinates less junk), and generation needs the
trellis.cpp weights resident, so ~8 GB of GPU memory is the practical
floor for making meshes. Repairing meshes needs no GPU at all.

## Why this exists

The author wanted alternatives to paid services and subscription programs.
Same capability — photo or prompt in, watertight print-ready STL out —
running entirely on your own machine. No cloud, no subscription, no account.

## The chain

```
words ──(phantasos, or your TXT2IMG_CMD)──► image
image ──► trellis.cpp server ──► textured GLB
GLB   ──► Z-up STL scaled to your stated mm
STL   ──► healed, watertight STL, ready to slice
```

Everything after the trellis.cpp server is native to the `gilgamesh` binary —
no Python, no Blender, no glue scripts to install.

## Quickstart

1. **Run the engine.** Build or download
   [trellis.cpp](https://github.com/pwilkin/trellis.cpp) (prebuilt Vulkan /
   ROCm / CUDA binaries on its releases page) and start its HTTP server on
   `:8080` per its README. GilgaMESH talks to `TRELLIS_URL`, default
   `http://127.0.0.1:8080` — if the server runs on another machine or
   another port, set it (`TRELLIS_URL=http://otherbox:8080 gilgamesh`).
   A chain that hangs at `[trellis]` is almost always this.
2. **Run `gilgamesh`.** No arguments opens the window: pick an image (or
   type a prompt), set a height in mm, watch the stages run live. Output
   lands in `~/GilgaMESH` (override with `GILGAMESH_OUT`).

Prefer the command line? The same chain runs headless behind a
subcommand:

```bash
gilgamesh chain ~/Pictures/boat.png 120   # picture -> 120mm-tall STL
gilgamesh chain "a small tugboat"         # words (needs phantasos or TXT2IMG_CMD)
```

Text-to-mesh is **optional**. Image mode needs only the trellis.cpp server.
The words path needs a text-to-image backend on top: either
[Phantasos](../phantasos) (its sibling module) on your `PATH`, or
`TXT2IMG_CMD` pointing at any command that takes `PROMPT OUT.png`. With
neither installed, a prompt fails loud with that message; a photo still
works.

There is also a free-standing repair tool — any STL in, watertight STL out,
no server needed:

```bash
gilgamesh remesh IN.stl OUT.stl [VOXEL_MM] [CLOSE_MM] [--mm HEIGHT]
```

And a headless snapshot — any STL to a shaded PNG on a transparent
background, CPU only, no window, no GPU:

```bash
gilgamesh render IN.stl OUT.png                          # 1024x1024, yaw 30°, pitch -12°
gilgamesh render IN.stl OUT.png --size 1600x900 --yaw 45 --pitch -20
```

- `--size WxH` — output pixels, both > 0. Default `1024x1024`.
- `--yaw D` — camera orbit around the model's vertical axis, degrees.
  Default `30`.
- `--pitch D` — camera elevation, degrees; negative looks down at the
  model. Default `-12`.

You get three files: `NAME.glb` (textured, for any 3D program), `NAME.stl`
(raw, at your stated size), `NAME-watertight.stl` (the one you slice).

Environment knobs, all optional:

| var | default | meaning |
|---|---|---|
| `TRELLIS_URL` | `http://127.0.0.1:8080` | where the trellis.cpp server lives |
| `TRELLIS_OUT` | current directory | where `gilgamesh chain` (the CLI) writes its three files. The window ignores it and uses `GILGAMESH_OUT` (default `~/GilgaMESH`) |
| `TXT2IMG_CMD` | unset | any command taking `PROMPT OUT.png` — overrides the words path. Without it, words render through Phantasos (its sibling module) (`phantasos shape`) if it's installed |
| `GILGAMESH_VOXEL` | `0.35` | (chain path only) remesh resolution in mm — finer keeps more detail, costs time and memory. `gilgamesh remesh` takes voxel/close positionally instead |
| `GILGAMESH_CLOSE` | `0.8` | (chain path only) closing radius in mm — how big a tunnel gets sealed |
| `GILGAMESH_MIN_WALL` | `0.8` | minimum thickness (mm) given to healed thin sheets — two 0.4mm perimeters. Both paths (chain and `remesh`); floors at 2.2× the voxel so the field math still has cells to work with |
| `GILGAMESH_SEED` | hash of the input image | reconstruction seed sent to trellis.cpp. Unset, the same picture reproduces the same mesh; set an integer to pin a run or re-roll one that came out as fragment soup |
| `GILGAMESH_RES` | unset (server default) | reconstruction resolution passed to the server (`512`, `1024`, `1536`) when its build supports it. `512` is the light-chain setting for 8 GB cards |

Developer / debugging knobs — not needed to use the tool, documented so
the output makes sense when you reach for them:

| var | meaning |
|---|---|
| `GILGAMESH_DUMP_DROPPED=<dir>` | the remesh writes every discarded body bigger than 5% of the keeper into `<dir>` as STLs, so "did it throw away a wall?" is answered by eye, not inference. Both paths |
| `GILGAMESH_WALL_REPORT` | set (any value) to print an **experimental** thin-wall estimate after the remesh. Truthful but not yet calibrated to the walls you care about — repair-seam remnants dominate the thin tail — so it stays quiet by default. Both paths |
| `GG_REAL_GLB=<file.glb>` | test-only: input for the ignored test `real_glb_through_native_remesh` (`cargo test --release -- --ignored real_glb`), which pushes a real reconstruction GLB through the native remesh and prints timings. Does nothing in the binary |

## Two lessons this repo paid for

**The axis lesson.** glTF is Y-up by spec; slicers and printers are Z-up.
Miss this and every model you print arrives lying on its back. The rotation
in the GLB→STL step is *unconditional* — the convention belongs to the
exporter, not the model, and "orient by longest axis" heuristics fail on real
files (a mech with an outstretched arm measures Z-longest while still being
Y-up). And note: a round-trip export→import test can **never** catch a
producer axis bug, because the two conversions are exact inverses. Only a
foreign file tests it.

**The watertight lesson.** Resampling beats hole-patching. Raw generative
meshes look great and slice terribly — one measured example arrived as 9
loose bodies with ~254 microscopic tunnels that read as holes in Cura. A
plain voxel remesh keeps the tunnels; morphological closing seals them but
washes out surface detail. So the native remesh does both jobs with the
tool that owns each: **closing owns the topology** (sealing tunnels for
good), **the detail snap owns the surface** (every vertex pulls back toward
the pristine import, so grooves return and former tunnels become shallow
dimples, not holes), and a final fine pass restores manifoldness.
Hallucinated zero-thickness sheets — reconstruction's favorite trick on
the side of the model the camera never saw — get healed to a printable
minimum thickness. Dust is dropped; anything model-sized stays, loudly,
even when the reconstruction orphaned it from the hull.

## Plain limits

Honesty over marketing. GilgaMESH resamples reconstructed geometry into a
printable solid — that trade has edges, and you should know them:

- **Thin walls are the hard case — state your real print size.** Truly
  zero-thickness hallucinated sheets get healed to a printable minimum
  automatically. But walls the reconstruction built at genuine sub-nozzle
  thickness are kept faithful — and a slicer will silently skip a wall it
  can't fit two lines into. The size you pass the chain (or `remesh
  --mm`) is a promise about printability at that size: print smaller than
  you stated and thin features drop out. Printing larger always helps,
  and your slicer's thin-wall mode buys margin. Check enclosed features
  (cabins, fins, panels) in the preview before printing.
- **Run it twice, get cousins, not twins.** The same input produces very
  slightly different meshes run to run (triangle counts wander a few
  percent). Every output is watertight and dimensionally faithful; the
  differences live below what a printed part shows. Don't build anything
  on "the same file, byte for byte."
- **Detail below the resample size washes out.** Fine grooves and sharp
  corners come back slightly softened. That's the price of guaranteed
  watertight.
- **Loose debris is discarded; real pieces are kept.** Reconstruction
  junk — floating specks disconnected from the main body — gets culled.
  Anything model-sized that overlaps the model or stands free is kept as
  a separate shell and reported (a free-floating one is your cue to
  eyeball before printing). A model-sized shell trapped fully INSIDE the
  body is dropped, loudly: slicers read nested shells as cavities, and a
  surprise hollow mid-print is worse than solid plastic.
- **Big openings stay open, on purpose.** A doorway is not a hole. Only
  small tunnels and pinholes get sealed; if your model is missing a wall
  it never had, no remesh invents one.

It still takes a photograph to a sliceable, watertight STL on your own
hardware for free. Know the edges, and it's a damned fine tool.

## What the paid services charge for

Meshy, Neural4D and friends sell "watertight STL from an image" as a
subscription feature. This repo is that feature, as one binary, on your
own GPU — including AMD cards the Python/CUDA stacks won't touch.

## Credits

- [microsoft/TRELLIS.2](https://github.com/microsoft/TRELLIS.2) — the model.
- [pwilkin/trellis.cpp](https://github.com/pwilkin/trellis.cpp) — the
  local C++/GGML engine this rides on.

[PolyForm Small Business 1.0.0](LICENSE.md) — free for individuals and
small shops. Print things.

If this saved you a subscription and you've got a few spare bucks:
[ko-fi.com/3DJ77](https://ko-fi.com/3DJ77). Appreciated, never required.
