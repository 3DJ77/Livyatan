# Glyptica 0.1.0 — 2026-09-12

First public release. Glyphs into matter: artwork in, cut linework and carved relief out.

- One window, the whole chain: **Open artwork…** takes a phone photo of a page, a scan,
  a clean PNG, an SVG, or a DXF. A photograph is thresholded into linework on open.
- Photo tools: **Flatten: click 4 corners** un-warps a hand-held photo; **Invert** for
  light strokes on dark stock; **min stroke area** drops dust.
- Mask tools: thicken, thin, close gaps, despeckle; pencil and eraser; Undo / Redo
  (Ctrl+Z / Ctrl+Y); **Reset to base image** returns to the artwork as opened.
- Place with the amber handles (4 or 9 nodes). The workpiece is square until artwork
  loads, then takes the artwork's own shape.
- **Export linework SVG** for a laser or plasma cutter's own software, or **Carve STL**:
  one closed relief slab in the art's shape, **Intaglio** (cut in) or **Emboss** (raised),
  with workpiece height, slab thickness, and engrave depth as number boxes (sliders on a toggle).
- The same chain as commands, each step a file you can inspect: `rectify`, `adjust`,
  `extract`, `refine`, `trace`, `place`, `emboss`. `glyptica --help` lists every flag.
- Tier 1: any Debian box. No GPU, no network, no account.

Known: photo detection is a mid-tone count, so a very clean high-contrast photo may pass
through as linework (the CLI `extract` always thresholds). The slab is flat; putting relief
onto a curved or tapered part is Structor's boolean job. Units are millimetres throughout.
