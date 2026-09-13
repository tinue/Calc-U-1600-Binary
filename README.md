# Calc-U-1600 — Qt6 prototype binaries

This repository hosts **pre-built binaries only**, for early feasibility
testing of a Qt6/C++ port of [Calc-U-1600](https://github.com/tinue/Calc-U-1600),
a Sharp PC-1500 / PC-1500A / PC-1600 pocket-computer emulator. The
production app is a native SwiftUI app (macOS/iOS); this Qt6 build is a
scoped-down prototype exploring a cross-platform (macOS/Linux/Windows) port.

**The source code is not public yet.** This repo exists purely so a small
number of people can try the prototype on Linux and Windows without
building it themselves. There is no installer, no code signing, and no
guarantee of stability — expect rough edges.

## Quick Start

1. Download the build for your platform from the table below, and also
   either grab a source-code zip of this repository or `git clone` it —
   either way, you need it for the preset files under `examples/`.
2. Start the emulator, then open **Settings** and set the path to the
   preset files (the `examples/` folder from step 1) and the path for
   the memory-card persistent files (any folder you'd like the emulator
   to save memory-module contents to between sessions).
3. Load the `lissajou-1600` preset to see it run — a quick first success
   before exploring further.

## What works

The emulator itself is the same core that drives the production SwiftUI
app — **full emulation, no limits there**: all three models (PC-1500,
PC-1500A, PC-1600) run for real, not a simulated subset.

The artwork and keyboard interaction are already as good as they're going
to get:

- Faceplate art for all three models, resizable with the window while
  keeping correct proportions.
- A live-rendering LCD — dot matrix plus the full status-indicator strip.
- Clickable on-screen keys, and full host-keyboard typing support
  (including SHIFT-tapped symbols and the PC-1600's own digit-row second
  legend, `' [ ] `` { } \ ~ _ | ^`).
- Model switching and Reset / ALL RESET.

## Memory modules

Memory modules are now selectable. Two of them are the real
[Soigeneris PC-1500 memory modules](https://www.soigeneris.com/sharp-pc-1500-memory-modules)
— module names and firmware are used with Soigeneris's permission — and
come with their firmware pre-installed when selected, just like the
physical modules do.

Example presets are included under `examples/`:

- `examples/setup/firmware_bootstrap_utilrm_20.pc1500a` demonstrates
  recovering a messed-up CE-163F back to factory state. The same
  procedure applies on original hardware.
- `examples/maxed-out-mem.pc1600` shows a PC-1600 with fully maxed-out
  memory. The module is pre-formatted and can't be re-initialized with
  `INIT` from the PC-1600 ROM, because its volume tables only go up to
  256k and this module is 512k — it was manually patched to 512k rather
  than produced through the normal `INIT` path.
- `examples/lissajou-1500.pc1500`, `examples/lissajou-1600.pc1600` and
  `examples/lissajou-ce150-1600.bas` (loaded via
  `examples/lissajou-ce150.pc1600`) draw a Lissajous figure on the
  built-in LCD or on a CE-150 plotter/printer, one per model — a quick
  way to see graphics output working.
- `examples/memtest_ce155.pc1500` runs a memory test against a CE-155
  module loaded through the universal software-defined card mechanism.
- `examples/memtest_bank.pc1500a` runs a memory test over all banks of
  a CE-163-style banked low-16K memory module on the PC-1500A.

The settings let you predefine a loader path for presets, and a save
path for memory-backed modules (so a module's contents persist to a
file of your choosing between sessions).

## Current limits

Two, for now: the **CE-158** RS-232 interface peripheral for the
PC-1500 and PC-1500A, and the **PC-1600F** floppy disk drive, are not
implemented. Aside from that, the core emulation itself is complete and
accurate. Any future additions are not to the core emulation, but to the
surroundings around it — e.g. the debug panel.

(On macOS/Linux, the builds are also plain executables rather than
signed, double-click-ready apps — see the platform notes below.)

## Downloads

Latest build (commit
[`a7e6d09`](https://github.com/tinue/Calc-U-1600/commit/a7e6d097d999f6d4fc7ab638f3c842188366a63b)
on the `qt6-prototype` branch):

| Platform | Download | Notes |
|---|---|---|
| Windows (x86_64) | [Calc-U-1600-Qt6-windows-x86_64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11-b/Calc-U-1600-Qt6-windows-x86_64.zip) | Self-contained — Qt runtime and the MSVC redistributable are bundled. Unzip anywhere and run `CalcU1600Qt.exe`. |
| Linux (x86_64) | [Calc-U-1600-Qt6-linux-x86_64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11-b/Calc-U-1600-Qt6-linux-x86_64.zip) | Requires Qt6 already installed (`qt6-base-dev` + `qt6-wayland` on a Wayland desktop, via apt or your distro's equivalent). Unzip, `chmod +x CalcU1600Qt`, run. |
| Linux (arm64) | [Calc-U-1600-Qt6-linux-arm64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11-b/Calc-U-1600-Qt6-linux-arm64.zip) | Same requirements as above (e.g. Raspberry Pi OS 64-bit). |
| macOS (Apple Silicon) | [Calc-U-1600-Qt6-macos-arm64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11-b/Calc-U-1600-Qt6-macos-arm64.zip) | Requires Qt6 already installed (`brew install qt`). It's a bare executable, not a `.app` — unzip, `chmod +x CalcU1600Qt`, then `xattr -d com.apple.quarantine CalcU1600Qt` (unsigned, so Gatekeeper blocks it otherwise) and run from a terminal. |

All builds come from the same commit; see the
[GitHub Actions run](https://github.com/tinue/Calc-U-1600/actions/runs/34589914038)
that produced them.

## Feedback

This is a feasibility test, not a release — if you try it, bug reports and
impressions are welcome, but please don't expect the missing features
above to show up here without a heads-up first.
