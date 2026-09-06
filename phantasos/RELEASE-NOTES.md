# Phantasos 0.3.0 — 2026-09-05

- First run finds a shared weights store (`<mount>/models/image` or `~/models/image`)
  instead of offering to download weights the machine already has; if there is none, it
  asks which models to download and fetches them.
- Window: top bar in three rounded panes (file / build / nav-ui, Structor's layout), prompt
  column on the left (multi-line, wraps, scrolls), picture on the right; an hourglass turns
  while a render or fetch runs; Save as… / Export… through the system file dialog.
- Server button: render on an sd-server elsewhere on the LAN (`host:port`) instead of
  loading a model on this machine.
- **Weights: <folder>** button: point Phantasos at weights you already have (a shared
  drive, another machine) instead of downloading 12–68 GB; the status line says what is
  installed there before you press Fetch. Saved to `~/.config/phantasos/model_dir`;
  `PHANTASOS_MODEL_DIR` overrides it.
- The big button is **Create Image**.
- Fetch shows live progress (`12.4 GB of 27.4 GB (45%)`) and refuses stray arguments.
- FLUX.2 klein and FLUX.2 dev each keep their own `flux2-vae.safetensors` (two different
  files with one name used to overwrite each other).
- Fixed: the Model and Open-in buttons shrank their label after one click.
- Look: Solarized palette shared by the whole suite, larger text, A+ / A- text scale.
