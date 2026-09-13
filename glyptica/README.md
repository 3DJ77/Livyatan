# Glyptica

**Glyphs into matter.** Artwork in; cut lines and carved relief out. A
module of the [Livyatan Design Suite](https://3dj77.github.io).

Photograph a drawing, a rubbing, a child's sketch, a page of lettering.
Glyptica flattens the page, pulls the linework off it, lets you clean and
place it, then hands you two things a machine can make: SVG linework for
a laser or plasma cutter, and a relief slab STL in the artwork's own
shape, ready to print or to boolean onto any part in Structor. Named for
glyptics, the old art of carving figures into stone.

The window sizes itself to the screen it opens on (a 4K monitor gets a
larger UI); `~/.config/livyatan/ui-scale`, if present, overrides that.

## Tier

**Tier 1 — any Debian box** with a display. No GPU, no network, no
accounts. Everything runs local; nothing phones home.

## Screenshot

![Glyptica window: a photographed page flattened and thresholded, placed on the workpiece, with photo tools, mask tools, and the two exports](assets/shot-window.png)

## Quickstart

```
sudo apt install ./glyptica_<version>_amd64.deb
glyptica                 # the window
glyptica photo.jpg       # the window, with your artwork open
```

Start to finish, in the window:

1. **Open artwork…** — a phone photo of a page, a scan, a clean PNG, an
   SVG, or a DXF. A photograph is thresholded into linework on open; clean
   linework passes straight through.
2. **Photo tools** (shown only for photographs): **Flatten: click 4
   corners**, then click the page's corners on the canvas, top-left,
   top-right, bottom-right, bottom-left. The page un-warps. **Invert** for
   light strokes on dark stock; **min stroke area** drops dust.
3. **Mask tools**: thicken, thin, close gaps, despeckle; pencil and eraser
   via **Cycle tool**; Ctrl+Z undoes.
4. Drag the amber handles to place the art on the workpiece. The workpiece
   is square until artwork loads, then takes the artwork's own shape.
5. **Export linework SVG** for the cutter, or pick **Intaglio** (cut in) or
   **Emboss** (raised), set **workpiece height** and **slab thickness**, and
   **Carve STL**. Both land beside your source file.

The same chain as commands, each step a file you can inspect:

```
glyptica rectify photo.jpg flat.png --quad x1,y1,x2,y2,x3,y3,x4,y4
glyptica adjust flat.png flat.png --gamma 0.8  # optional: lift a dim photo
glyptica extract flat.png mask.png            # adaptive threshold -> stroke mask
glyptica refine mask.png mask.png --close 2   # optional cleanup
glyptica trace mask.png art.svg               # linework for the cutter
glyptica emboss mask.png relief.stl --mm 220  # relief slab, 220 mm tall
```

Every flag, by step (`glyptica --help` prints the same list on stderr):

| step | flags |
|---|---|
| `rectify` | `--quad x1,y1,…,x4,y4` (page corners, TL TR BR BL) · `--size WxH` (output pixels, default 520x2080) · `--vstretch S` (multiply output height) |
| `adjust` | `--gamma G` · `--levels lo,hi` (0–1 black/white points) |
| `extract` | `--min-area N` (drop blobs under N px of area, default 60) · `--invert` (light strokes on dark) · `--crop x,y,w,h` |
| `refine` | `--dilate N` · `--erode N` · `--close N` (N = 3×3 passes, max 64) · `--min-area N` (drop blobs under N px of area) |
| `trace` | `--speckle N` (ignore specks under N px, default 8) |
| `place` | `--offset dx,dy` · `--scale sx,sy` · `--shear s` — all as fractions of the face (`--offset 0,0.02` = 2% down); writes a PNG preview of the placement |
| `emboss` | `--mm H` (slab height, default 220; width follows the art's aspect) · `--thick T` (slab thickness, default 6) · `--depth D` (relief mm, default 1.5) · `--raise` (emboss: strokes stand proud; default is intaglio, cut in) · plus the `place` flags |

## What it makes

- **SVG linework** — for a laser or vinyl cutter's own software, or for
  Hephaestus/Structor to consume.
- **Relief slab STL** — one closed solid in the art's own shape. Print it,
  or boolean it onto a part in Structor.
- **Masks** — Ctrl+S saves the edited mask as `<name>-edit.png`; **Save
  warped mask** saves it with the placement baked in.

## Limits, honestly

- The slab is flat. Wrapping relief onto a curved or tapered surface is
  Structor's job (boolean the slab onto the part).
- Photo detection is a mid-tone count: a very clean, high-contrast photo
  may pass through as linework. The CLI `extract` always thresholds.
- SVG text renders with your system fonts; an SVG referencing a font you
  don't have falls back like a browser would.
- Input images cap at 64 megapixels — downscale first if you're feeding
  it scanner plates.
- The file picker uses `zenity` or `kdialog` if present; without them,
  pass the path on the command line (`glyptica art.png`).

## Installed files

The `.deb` puts nothing outside the standard system tree. Everything it
installs:

```
/usr/bin/glyptica
/usr/share/applications/glyptica.desktop
/usr/share/doc/glyptica/README.md
/usr/share/doc/glyptica/RUNBOOK.md
/usr/share/doc/glyptica/THIRD-PARTY-LICENSES.md
/usr/share/doc/glyptica/changelog.gz
/usr/share/doc/glyptica/copyright
/usr/share/icons/hicolor/256x256/apps/glyptica.png
/usr/share/man/man1/glyptica.1.gz
/usr/share/glyptica/assets/splash.jpg
/usr/share/glyptica/data/resources.registry
/usr/share/pixmaps/glyptica.png
```

Remove with `sudo apt remove glyptica`; nothing is left behind.

## License

[PolyForm Small Business 1.0.0](LICENSE.md) — free for individuals and
small shops. Third-party attributions: [THIRD-PARTY-LICENSES.md](THIRD-PARTY-LICENSES.md).
