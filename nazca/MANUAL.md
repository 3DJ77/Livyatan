# Nazca — Operator Manual

3D toolpath and slice-file viewer of the Livyatan Design Suite. Sovereign,
local-first, Rust + fyrox. PolyForm Small Business license.

## Quickstart

```
nazca path/to/job.nc
nazca path/to/print.ctb
```

One CLI argument: the file. No argument → empty scene; hit **Load**
(top-left panel) for a zenity picker filtered to `*.nc *.gcode *.ngc *.tap *.ctb`.
Anything not ending `.ctb` is parsed as G-code.

Camera (Chimaera orbit): **right-drag** orbits, **wheel** zooms. Close the
window to quit.

Colors, G-code view. The file's machine is detected (E words = 3D printer;
spindle power with no downward feed = laser, plus a dwell after M3 = plasma;
otherwise router) and the legend names that machine's move classes:

| machine | classes and colors |
|---|---|
| 3D printer | travel blue · extrude green · support light amber · retract purple · purge/skirt orange |
| router / mill | rapid blue · plunge purple · cut red · arc orange · drill cycle teal · lead-in orange-red dotted |
| laser | travel blue · cut red · engrave orange · frame (beam off) green |
| plasma | travel blue · pierce teal · cut red · torch off white · THC Z yellow |

Support, purge, and lead-in come from slicer/CAM comments (`;TYPE:SUPPORT`,
`;TYPE:SKIRT`, `(lead in)`); without them those moves fall back to their
parent class. G90/G91 absolute and relative motion are both honored;
G81–G83 drill cycles expand to rapid-over, feed-down, retract.

The panel shows filename, move count, per-class tallies, and the
bounding box in mm. Everything also echoes to stdout as `NAZCA …` lines.

## What it is

Walk the lines before the machine does. Nazca reads suite output — the
G-code a post produced, the .ctb a slicer wrote — and draws it in 3D so you
can eyeball the path before metal or resin is on the line. Moves are drawn as
square tubes, not lines, so the path reads from any camera angle. It is a
viewer only: it never edits, never sends, never talks to a controller.

## Why the name

The Nazca lines are toolpaths at landscape scale: single continuous paths
laid across a plain, and the running theory is that people walked them as
a form of preparation or meditation before what came next. A toolpath is
the same thing at bench scale, and getting it wrong costs you. This viewer
walks the lines first. (Two earlier names retired.)

## Features

- **G-code parse** (`src/parse.rs`, pure and headless, 3 tests):
  - Words: X/Y/Z coords, G modal group 0–3, I/J arc centers. Modal position
    and modal G carry line to line. Absolute (G90) assumed — that's what the
    suite emits.
  - **Arcs: I/J-center G2/G3 yes** — interpolated to ≤0.3 mm chords in the XY
    plane at current Z. **R-form arcs no** — they draw as a straight cut.
  - Plunge detection: a G1 with no XY motion and descending Z (router jobs).
- **.ctb decode** (Jove's unencrypted v4/v5 shape): magic check, header stats
  (layers, layer height, total height, exposure, resolution) from fixed
  offsets, plus the embedded RGB15-RLE large preview rendered top-right.
- **3D render**: one tube mesh per move class, auto-centered and
  auto-framed; tube radius scales with job extent. Dark floor slab, one
  directional light.

## Using it

- Point it at any `.nc` output, orbit, and check three things:
  plunges land where you meant them, rapids clear the stock, and no arc
  collapsed into a straight line (that's an R-form arc — see Known limits).
- For a `.ctb`, you get the header numbers and the preview thumbnail — enough
  to confirm you grabbed the right file, not enough to verify layers.
- Loading a second file (button or picker) clears the old view first.
- The parser tests run headless: `cargo test 2>&1 | tail -3`.

## How it connects

- **Hephaestus** — CAM `.nc` programs: the main diet.
- **Any post's G-code** — laser/plasma programs load here in 3D too.
- **Jove** — `.ctb` files; `parse.rs` decodes the exact inverse of Jove's
  preview encoder.

## Known limits

A viewer that misdecodes is worse than no viewer — you'd trust a wrong
picture. These are real, open, confirmed in the current code:

- **G92/G28/G10 are not understood.** They don't update `modal_g`, so their
  coordinate words are decoded as motion under whatever G0–G3 was last
  active. A `G92 X0 Y0` will draw a phantom move. Programs using work-offset
  or homing lines will backplot wrong.
- **Parenthetical comments are scanned as moves.** Only `;` comments are
  stripped. A `(TOOL CHANGE X5)` comment parses its X5 as a real coordinate.
  Strip paren comments from files before trusting the plot.
- **Encrypted v5 .ctb is accepted but decoded from the wrong offsets.** The
  encrypted magic passes the check and header stats are read from the
  unencrypted layout — the numbers shown are garbage presented as real. The
  preview is skipped, but don't trust any stat from an encrypted file.
- R-form arcs draw straight (by design for now — queued below).
- No G91 (relative) support; incremental programs plot wrong silently.

## Queued

- **.ctb layer RLE scrubbing** — decode the layer masks for a slider through
  the stack (header + preview only today).
- **R-form arcs** — expand G2/G3 R… properly instead of drawing straight.
- **Move-order playback** — a slider stepping through the path in time.
- **Per-class visibility toggles** — declutter dense jobs.
