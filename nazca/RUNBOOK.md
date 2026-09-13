# Nazca — Runbook

*See the cut before you make it. Tier 1 — any Debian box.*

## Scrubbing

- 3D job: the vertical bar on the right is the layer scrubber; the box
  above it takes a layer number. Flat job: the bar along the bottom steps
  through moves; the box at its right end takes a move number.
- **Play** (bottom-right corner) runs the active scrubber to the end;
  press again to stop. Dragging a bar stops playback.
- Resin `.ctb`: **3D stack** (under the legend) builds a voxel stack of
  every layer once, then the layer bar and Play grow the form in 3D.

## Install and launch

```
sudo apt install ./nazca_<version>_amd64.deb
nazca part.nc
```

## The five-minute tour

- Orbit with the mouse; the path draws rapids and cuts in different
  colors named in the legend for the machine the file is for.
- The panel reads the file's vitals — for a `.ctb`: layers, layer
  height, total height, exposure, pixel grid.
- **Load** (zenity) or pass a path on the command line.

## Worked example — and the chain

Cut files from **Hephaestus**, sliced vats from **Jove**:

```
hephaestus profile part-outer.json -o outer.nc --tool 1.5
nazca outer.nc        # walk it — then cut it

jove --masks stack.raw --layers 800 --layer-height 0.05 --out part.ctb
nazca part.ctb        # check layers/exposure — then print it
```

Nazca is the pause between the design bench and the machine: the
place you catch the wrong-side comp or the absurd layer count while it
still costs nothing.
