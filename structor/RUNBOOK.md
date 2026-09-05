# Structor — Runbook

*Design module. Tier 0 — any Debian box, no GPU, no network, no account.*

## Install and launch

```
sudo apt install ./structor_<version>_amd64.deb
structor
```

The window opens on an empty build plate under a night sky.

## The ten-minute tour

- **Drop a solid**: click a palette button (top-left) — thirteen
  primitives from BOX to GEAR (set teeth and module first for a gear).
  It lands on the plate; the SELECTED panel below the palette shows its
  exact position, rotation, and size for numeric entry.
- **Move it**: left-drag the solid. It slides on the plate and snaps to
  the grid; corners and face-centers catch on other parts' feature
  points (hold **Ctrl** for precision, no snap).
- **Rotate**: drag the rings around the selected solid.
- **Scale**: grab the bounding-box handles — corners scale uniformly,
  face handles scale one axis.
- **Look around**: right-drag orbits, wheel zooms, middle-drag pans.
  A SpaceMouse works out of the box; the NAV panel tunes the feel and
  remembers it.
- **Axis views**: click a triad glyph to snap to a standard view;
  click again for the opposite side.

## The worked example — the suite bracket

This bracket is the thread that runs through every module runbook: what
you make here gets sliced in Jove next drop.

1. **Back plate**: drop a BOX, scale it to 60 x 60 x 6 mm flat on the
   plate.
2. **Shelf**: drop a second BOX, 60 x 40 x 6 mm, rotate it 90° so it
   stands on the back plate's top edge, and slide it flush.
3. **Gusset**: drop a WEDGE, scale to 30 x 30 x 6 mm, and set it into
   the corner between plate and shelf.
4. **Screw holes**: drop two CYLINDERs, 5 mm diameter, taller than the
   back plate. Push each through the plate where a screw goes, then
   press **H** with the cylinder selected — it goes ghost-blue: it is now a
   HOLE, cut from whatever it overlaps.
5. **Merge**: select everything and merge — the preview IS the result;
   Structor uses the same boolean engine OpenSCAD does, so what you
   see is what exports.
6. **Save + export**: **SAVE** (Ctrl+S) writes `bracket.SigN` into
   `~/Structor` (a readable JSON-CSG spec, not a blob — open it in a text
   editor and see your tree; **OPEN** / Ctrl+O brings it back). **EXPORT
   STL** writes `bracket.stl`, watertight. While you work, the scene
   autosaves to `~/Structor/autosave.SigN` once a minute.

Keep both files. Next module's runbook starts from `bracket.stl`.

## Files

| format | direction | what |
|---|---|---|
| `.SigN` | open + save | the scene tree as readable JSON-CSG |
| `.stl` | import + export | meshes in, watertight resolved solid out |
| `.obj` | export | same solid for tools that prefer OBJ |

## Developer knobs

Test-only; the shipped binary never reads them.

- `SHOP_TEST_DIR=<dir>` — where `cargo test` writes the shop-export end-to-end
  output (MANIFEST.txt, bom.csv, cut files) instead of `$TMPDIR/structor-whips-e2e`,
  so the files can be inspected after the run.

## Troubleshooting

- **Nothing exports** — an empty scene exports nothing; check something
  is on the plate and not marked as a hole.
- **A hole didn't cut** — the hole solid must actually overlap the body
  it cuts, and both must be in the merge selection.
- **Mouse feel is wrong** — open the NAV panel and tune orbit / pan /
  zoom sense and inversion; it persists per user.
- **Undo** — Ctrl+Z walks history back; every drag/rotate/scale is a
  checkpoint.
