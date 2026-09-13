# Glyptica — Runbook

*Artwork -> cut linework and carved relief. Tier 1 — any Debian box, no
GPU, no network.*

## Install and launch

```
sudo apt install ./glyptica_<version>_amd64.deb
glyptica
```

Bare `glyptica` opens the window; `glyptica --help` lists the CLI.

## The five-minute tour

- **Open artwork…** picks a photo, scan, PNG, JPG, SVG, or DXF (or launch
  as `glyptica photo.jpg`). A photograph is thresholded into linework on
  open and the **photo tools** appear.
- **Flatten: click 4 corners** — click the page corners on the canvas
  (top-left, top-right, bottom-right, bottom-left); the page un-warps and
  re-thresholds. **Invert** for chalk on slate; **min stroke area** for dust.
- **Mask tools** thicken, thin, close gaps, despeckle. **Cycle tool** gets
  you pencil and eraser; Ctrl+Z undoes.
- Drag the **corner handles** to place and warp the art on the workpiece.
  The workpiece is square until artwork loads, then takes its shape.
- **Export linework SVG** writes `<name>-lines.svg` beside the source.
- **Intaglio** cuts the strokes into the face; **Emboss** raises them. The
  preview darkens or lightens the strokes to match. **Workpiece height** and
  **slab thickness** size the STL; **Carve STL** writes one closed relief
  slab beside the source. The status line names every file it writes.
- Ctrl+S saves the edited mask as `<name>-edit.png` — reload it to
  continue where you left off.

## Worked example — and the chain

Take a phone photo of a drawing. In the window: Open artwork, Flatten
(four clicks), Export linework SVG, Emboss STL. Or as commands:

```
glyptica rectify photo.jpg flat.png --quad 132,88,1870,102,1844,2610,158,2596
glyptica adjust flat.png flat.png --gamma 0.8 --levels 0.1,0.9   # dim photo? lift it
glyptica extract flat.png mask.png --min-area 40                  # --invert for chalk on slate
glyptica refine mask.png mask.png --close 2 --min-area 40         # --dilate/--erode N to fatten/thin
glyptica trace mask.png art.svg --speckle 8
glyptica place mask.png preview.png --offset 0,0.02 --scale 0.9,0.9 # check placement, no STL yet
glyptica emboss mask.png relief.stl --mm 220 --thick 6 --depth 1.5 --offset 0,0.02 --scale 0.9,0.9   # --raise for emboss
```

Knobs you will actually reach for: `--size WxH` and `--vstretch S` on
`rectify` when the flattened page comes out the wrong proportion;
`--crop x,y,w,h` on `extract` to ignore the page edge; `--shear s` on
`place`/`emboss` when the art should lean. Offset, scale, and shear are
fractions of the face, not pixels.

`art.svg` is the chain link sideways — laser or vinyl linework. And
`relief.stl` chains forward: slice it for resin in **Jove**, or drop it
into **Structor** to boolean onto a part. The drawing on paper ends up in
matter — which is the whole point of the name.
