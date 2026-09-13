# GilgaMESH 0.2.1 — 2026-09-12

- The UI sizes itself to the monitor the window opens on; a saved `~/.config/livyatan/ui-scale` overrides it. Text + / Text − are gone.

## Previously, 0.2.0 — 2026-09-05

- Top bar in three rounded panes on one row (paper | rock | text size), 1600-wide window.
  Every button has a hover tooltip. On the server path
  `NAME-watertight.stl` is the server's mesh as-is: the native remesh only added rays and
  holes to it (`GILGAMESH_FORCE_REMESH=1` runs it anyway); a non-manifold server mesh also
  gets `NAME-remeshed.stl`, the native result, as a fallback.
- Docs now say the thing that decides model vs confetti: start `trellis-server` with
  `--birefnet` (background removal). Same photo measured: 1,760 loose bodies without it,
  51 with. The stage log prints a `[hint]` line when the remesh drops hundreds of bodies.
- **Rotate 90°** and **Crop to square** fix the picked photo before the run; the original
  is untouched.
- The menu icon was missing from the package; fixed.
- Look: Solarized palette shared by the whole suite, larger text, A+ / A- text scale.
- Tested end to end against a photo of a real printed object: 1 body, watertight,
  126,688 faces at 125 mm.

## State of this release — a working test prototype

We are releasing GilgaMESH early, as it stands, because the inaugural trio (Structor,
Phantasos, GilgaMESH) is more useful to makers together than each waiting for the
other. What is true today:

- **Works, tested this week:** photo → textured GLB + mm-scaled STL through the full
  chain on a big unified-memory box (AMD Strix Halo, 128 GB) running trellis-server with
  the studio weights and background removal (`--birefnet`). A photo of a printed
  obelisk came back as one watertight body; a photo of a truck came back at 14 million
  faces and sliced in Cura.
- **Known:** the server's mesh can carry non-manifold edges from its decimator. Slicers
  take it; the raw STL is the file to slice. A native-remeshed fallback
  (`NAME-remeshed.stl`) is written alongside in that case, and `GILGAMESH_FORCE_REMESH=1`
  forces the native pass. The native pass on very large meshes can add rays and holes —
  that is why it no longer runs by default on server output.
- **Known:** the words path (a description instead of a photo) needs Phantasos installed
  and a Klein image server reachable; on one GPU that server and trellis-server take
  turns. Documented, not polished.
- **Not re-tested this release:** the 8 GB "light chain" (geometry-only, `--no-texture
  --res 512`). It is documented from earlier measurements; expect confetti unless the
  server runs with background removal.
- **Hardware, plainly:** making meshes needs a GPU box with the trellis.cpp weights
  resident — about 8 GB of GPU memory is the floor, 128 GB unified memory is what we
  ship from. Repairing meshes (`gilgamesh remesh`) needs no GPU.

We know the rough edges and are working on them. Reports welcome.
