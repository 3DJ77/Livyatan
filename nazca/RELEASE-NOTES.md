# Nazca 0.1.0 — 2026-09-12

First public release. The viewer: walk the lines before the machine does.

- Loads G-code (`.nc .gcode .ngc .tap`) and sliced resin `.ctb`. It reads; it never
  writes, never sends, never talks to a controller.
- Detects the machine from the file and colours every move by class: **3D printer**
  travel / extrude / support / retract / purge; **router / mill** rapid / plunge / cut /
  arc / drill cycle / lead-in (dotted); **laser** travel / cut / engrave / frame;
  **plasma** travel / pierce / cut / torch off / THC Z. One show/hide button per class.
- Scrubbing: a **layer bar** down the right edge for 3D jobs, a **move bar** along the
  bottom for flat cuts, each with a number box; **Play** runs the job through in about
  twenty seconds. Scrubbing never rebuilds geometry, so it stays smooth on big files.
- Resin `.ctb`: every layer's mask decodes on demand and shows in green; **3D stack**
  voxelises the layers so Play grows the print under the orbit camera.
- G90/G91 absolute and relative motion honoured; G81–G83 drill cycles expanded;
  G2/G3 arcs with I/J centres; comments (`;` and parentheses) read for slicer/CAM tags.
- Chimaera camera: right-drag orbits, wheel zooms; **NAV** tunes the shared mouse feel.
- Tier 1: any Debian box with a display. No GPU, no network, no account.

Known: R-form arcs draw as straight cuts. Support, purge, and lead-in classes depend on
slicer/CAM comments and fall back to their parent class without them. Encrypted `.ctb`
(v5 magic 0x12FD0107) is refused, not misread. The 3D stack decodes every layer once
when toggled, a few seconds on a 1000-layer file.
