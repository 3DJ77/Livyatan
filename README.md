# Livyatan — release builds

Debian packages for the Livyatan desktop-manufacturing suite. Each module
is a separate program; they hand each other ordinary files. Everything runs
on your own machine — no account, no cloud, nothing phones home.

**This repository carries binaries only.** Source is not published yet; it
will be released later, module by module, as each one clears its release
gates. That is a deliberate choice, stated plainly, not an oversight.

## Modules here

| module | what it does | version |
|---|---|---|
| [GilgaMESH](gilgamesh/) | a photo in, a watertight mm-scaled STL out | 0.1.1 |
| [Phantasos](phantasos/) | image generation from a prompt or another image, local weights | 0.2.0 |

Each module directory holds its `.deb`, README, MANUAL, RUNBOOK and man page.

## Install

```
sudo apt install ./gilgamesh_0.1.1_amd64.deb
```

Debian 13 (trixie), amd64. Tested on: an 8 GB NVIDIA T1000 workstation
card, a Strix Halo with 128 GB unified memory, and a no-GPU desktop for the
window and CLI paths — the per-module README states what needs a GPU.

These are early cuts — 0.1 and 0.2 releases from one person's bench.

The wall: https://3dj77.github.io
