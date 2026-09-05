# GilgaMESH — Runbook

*Photo/prompt → mesh. Tier 2 — needs a real GPU (built and tested on AMD
Strix Halo, 128 GB unified) and a running trellis.cpp server on `:8080`
(or wherever `TRELLIS_URL` points). Text prompts additionally need
`phantasos` on `PATH` or `TXT2IMG_CMD`; photos need neither.*

## Install and launch

```
sudo apt install ./gilgamesh_<version>_amd64.deb
gilgamesh
```

The window opens on the GilgaMESH splash while it loads.

## The five-minute tour

- **Pick image…** opens a file picker (zenity/kdialog) for a photo. No
  picker installed? Type the path straight into the box next to it — the
  same box also takes a text prompt if `TXT2IMG_CMD` is set.
- **mm tall** sets the output height in millimeters (default 80).
- **Make solid** runs the chain and streams each stage live: paint (if a
  prompt), trellis reconstruction, STL scale, watertight remesh. This is
  minutes, not seconds — the splash and stage log are there so a long run
  never reads as a crash.
- Output lands in `~/GilgaMESH` (override with `GILGAMESH_OUT`): the
  textured `.glb`, the raw `.stl`, and `NAME-watertight.stl` — the one to
  slice, e.g. in Jove.

## Command line

The window's chain also runs headless, behind a subcommand:

```bash
gilgamesh chain ~/Pictures/boat.png 120
gilgamesh chain "a small tugboat"   # needs phantasos or TXT2IMG_CMD
```

The CLI chain writes its three files to `TRELLIS_OUT` (default: the
current directory), not to the window's `GILGAMESH_OUT`.

The remesh stage stands alone as a repair tool for any STL:

```bash
gilgamesh remesh IN.stl OUT.stl [VOXEL_MM] [CLOSE_MM] [--mm HEIGHT]
```

And `render` draws a headless snapshot of any STL — shaded PNG,
transparent background, CPU only, no window:

```bash
gilgamesh render IN.stl OUT.png [--size WxH] [--yaw D] [--pitch D]
```

`--size` defaults to `1024x1024`, `--yaw` (orbit, degrees) to `30`,
`--pitch` (elevation, degrees, negative looks down) to `-12`.

## Environment

All optional. Chain-only knobs are ignored by `remesh`; remesh knobs
apply to both the chain's remesh stage and the standalone subcommand.

| var | scope | default | does |
|---|---|---|---|
| `TRELLIS_URL` | chain | `http://127.0.0.1:8080` | the trellis.cpp server. Set it when the server is on another host or port |
| `TRELLIS_OUT` | `gilgamesh chain` only | `.` | where the CLI chain writes; the window uses `GILGAMESH_OUT` |
| `GILGAMESH_OUT` | window | `~/GilgaMESH` | where the window writes |
| `TXT2IMG_CMD` | chain, words | unset | command taking `PROMPT OUT.png`; without it words go through `phantasos shape` |
| `GILGAMESH_SEED` | chain | hash of the image | reconstruction seed; set an integer to pin or re-roll |
| `GILGAMESH_RES` | chain | server default | reconstruction resolution (`512`/`1024`/`1536`) if the server build supports it |
| `GILGAMESH_VOXEL` | chain remesh | `0.35` | voxel size, mm (`remesh` takes it positionally) |
| `GILGAMESH_CLOSE` | chain remesh | `0.8` | closing radius, mm (`remesh` takes it positionally) |
| `GILGAMESH_MIN_WALL` | both | `0.8` | minimum wall given to healed sheets, mm; floored at 2.2× voxel |
| `GILGAMESH_DUMP_DROPPED` | both, debug | unset | `=<dir>` writes every discarded body > 5% of the keeper as STLs |
| `GILGAMESH_WALL_REPORT` | both, debug | unset | set to print the experimental thin-wall estimate |
| `GG_REAL_GLB` | tests only | unset | input GLB for the ignored `real_glb_through_native_remesh` test; no effect on the binary |

## Troubleshooting

- **Hangs at `[trellis]`** — no trellis.cpp server answering on
  `TRELLIS_URL` (default `http://127.0.0.1:8080`). Start it first; if it
  is running on another box or port, export `TRELLIS_URL` to match.
- **`text mode needs phantasos installed, or TXT2IMG_CMD set`** — you
  typed a prompt and no text-to-image backend was found. Install
  Phantasos, set `TXT2IMG_CMD`, or feed it a photo instead.
- **Same photo, different mesh** — `[trellis]` prints the seed it used.
  Pin it with `GILGAMESH_SEED=<that number>`; change it to re-roll a
  reconstruction that came out as fragment soup.
- **"dropped N bodies" and something looks missing** — rerun with
  `GILGAMESH_DUMP_DROPPED=<dir>` and open the STLs it writes there.
- **Fails at `[remesh]`** — the remesh is native to the binary; a failure
  here is a bug, not a missing dependency. File it with the input STL.
- **Model prints lying on its back** — shouldn't happen; the Z-up
  correction is unconditional. If it does, it's a bug — file it.
