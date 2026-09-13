# Nazca

**Walk the lines before the machine does.** The toolpath and slice-file
viewer of the [Livyatan Design Suite](https://3dj77.github.io).

Load the `.nc` your CAM wrote or the `.ctb` your slicer packed, and see
exactly what the machine will do — travels, cuts, extrusions, layer stats —
before any iron moves or resin cures. It reads; it never writes.

## Walk it

A 3D job (a print, a router job with Z passes) gets a **layer scrubber**
down the right edge: drag it, or type a layer number in the box above it,
and the view shows everything up to that layer. A flat laser or plasma
job gets a **move scrubber** along the bottom, stepping through the cuts
and moves in program order, with a move number box at its right end. A
sliced resin `.ctb` gets the layer scrubber too: each layer's mask is
decoded and shown in green as you scrub or play. **3D stack** toggles a
voxel view of the same layers, so Play raises the form under the orbit
camera the way the print will grow; **2D layer** goes back to the mask.
**Play**, in the corner where the two meet, runs the active scrubber to
the end in about twenty seconds; Stop halts it.

## Tier

**Tier 1 — any Debian box** with a display. No network, no accounts,
nothing phones home, and the viewer has no save button by design.

## Quickstart

```
sudo apt install ./nazca_<version>_amd64.deb
nazca part.nc      # or bare `nazca`, then Load
nazca part.ctb     # sliced resin file: stats + preview
```

Reads G-code (`.nc`, `.gcode`, `.ngc`, `.tap`) and unencrypted ChiTu
`.ctb`. An encrypted v5 `.ctb` is refused with a clear message — a
checker that guesses is worse than one that says no.

## Honest limits

- The G-code walk covers G0–G3 with arcs; exotic dialect codes (G92
  offsets, G91 incremental mode) aren't simulated — a file leaning on
  them won't preview true. Check the panel numbers against your CAM.
- File picker wants `zenity`; without it, pass the file on the command
  line.

## Installed files

The `.deb` puts nothing outside the standard system tree. Everything it
installs:

```
/usr/bin/nazca
/usr/share/applications/nazca.desktop
/usr/share/doc/nazca/MANUAL.md
/usr/share/doc/nazca/README.md
/usr/share/doc/nazca/RUNBOOK.md
/usr/share/doc/nazca/THIRD-PARTY-LICENSES.md
/usr/share/doc/nazca/changelog.gz
/usr/share/doc/nazca/copyright
/usr/share/icons/hicolor/256x256/apps/nazca.png
/usr/share/nazca/assets/splash.jpg
/usr/share/nazca/data/resources.registry
/usr/share/man/man1/nazca.1.gz
/usr/share/pixmaps/nazca.png
```

Remove with `sudo apt remove nazca`; nothing is left behind.

## License

[PolyForm Small Business 1.0.0](LICENSE.md). Third-party attributions:
[THIRD-PARTY-LICENSES.md](THIRD-PARTY-LICENSES.md).
