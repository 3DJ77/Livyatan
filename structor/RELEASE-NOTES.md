# Structor 0.11.0 — 2026-09-05

First public release.

- Text + / Text − buttons resize the suite text (restart to apply).
- Save / Open / Recent on the toolbar (`.SigN`, default folder `~/Structor`); autosave
  once a minute to `~/Structor/autosave.SigN`; the title bar shows the file and a `*`
  while unsaved; closing with unsaved changes writes the autosave and asks to save.
- Hide / Show All, REST (drop a part onto the plate or onto another), FIT ALL, MEASURE,
  UNDO/REDO with depth, UNITS (mm / in) driving the inspector and readouts, BREAK (un-weld).
- Z is the part's base: Z = 0 rests it on the plate. New parts arrive at 25.4 mm with the
  keyboard already in their size fields. Parts list with hide/select per part.
- Top bar in three panes: file, build, view. Hover any button for its shortcut. Size
  inspector and parts list on the right. Every shape on the palette with a rendered icon.
- Look: Solarized palette shared by the whole suite; A+ / A- text scale for every module.
- Environment: the plate sits in a modelled space — SHOP 3D (a 30 m shop bay, the launch
  view: the build plate lies on a granite surface-plate inspection bench mid floor, a
  bridge crane rides under the trusses), HILLS 3D (open ground), SPACE 3D (a station bay) — so the view
  keeps true perspective from any angle. The older SHOP / HILLS / SPACE photo domes stay
  in VIEW. The operator places the environment around the plate with the SpaceMouse
  (MAGIC CARPET in the DEBUG pane) or VIEW > BG LEVEL; the placement is kept per
  environment in `~/.config/structor/backdrop.json`.
- Fixed: an installed Structor crashed on its first backdrop (absolute asset path);
  saves went to an unwritable directory under a package install; the seed part was a
  2 mm dot on a 300 mm plate; a SpaceMouse fly left HOME / FIT ALL dead.

Known: the machines in SHOP 3D and SPACE 3D are plain box stand-ins; modelled props come
in the first update.
