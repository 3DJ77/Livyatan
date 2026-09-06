# GilgaMESH 0.2.0 — 2026-09-05

- Every button has a hover tooltip. When the reconstruction server already returns a
  watertight mesh, `NAME-watertight.stl` is written as-is: the native remesh only ran on
  closed meshes to add rays and holes.
- Docs now say the thing that decides model vs confetti: start `trellis-server` with
  `--birefnet` (background removal). Same photo measured: 1,760 loose bodies without it,
  51 with. The stage log prints a `[hint]` line when the remesh drops hundreds of bodies.
- **Rotate 90°** and **Crop to square** fix the picked photo before the run; the original
  is untouched.
- The menu icon was missing from the package; fixed.
- Look: Solarized palette shared by the whole suite, larger text, A+ / A- text scale.
- Tested end to end against a photo of a real printed object: 1 body, watertight,
  126,688 faces at 125 mm.
