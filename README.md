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
| [Structor](structor/) | CAD bench: solids in, drawings and cut files out | 0.11.0 |
| [GilgaMESH](gilgamesh/) | a photo in, a watertight mm-scaled STL out | 0.2.0 |
| [Phantasos](phantasos/) | image generation from a prompt or another image, local weights | 0.3.0 |
| [Glyptica](glyptica/) | artwork in; SVG cut lines and a carved relief STL out | 0.1.1 (pre-beta) |
| [Nazca](nazca/) | the viewer: walk any G-code or resin job before the machine does | 0.1.1 (pre-beta) |

Each module directory holds its `.deb`, README, MANUAL, RUNBOOK and man page.

## Install

```
sudo apt install ./structor_0.11.0_amd64.deb
```

Debian 13 (trixie), amd64. Tested on: an 8 GB NVIDIA T1000 workstation
card, a Strix Halo with 128 GB unified memory, and a no-GPU desktop for the
window and CLI paths — the per-module README states what needs a GPU.

These are early cuts from one person's bench. GilgaMESH ships as a working test
prototype; Glyptica and Nazca are pre-beta and may have issues. Each module's
release notes say plainly what works and what does not.

## Reporting

Something broke, or installed wrong, or the manual lied? Open an issue on this
repository with the module, its version (`<module> --version`), your Debian/Ubuntu
version and GPU, and what you did. Screenshots help. Every report gets read.

The wall: https://3dj77.github.io
