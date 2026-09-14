# Calc-U-1600 — Qt6 binaries

This repository hosts **pre-built binaries only**, for early feasibility
testing of a Qt6/C++ port of [Calc-U-1600](https://github.com/tinue/Calc-U-1600),
a Sharp PC-1500 / PC-1500A / PC-1600 pocket-computer emulator. The
production app is a native SwiftUI app (macOS/iOS); this Qt6 build is a
scoped-down prototype exploring a cross-platform (macOS/Linux/Windows) port.

**The source code is not public yet.** This repo exists purely so a small
number of people can try the prototype on Linux, macOS, and Windows
without building it themselves.

**This is a packaging test release.** The point of this drop is to check
that the installer / `.dmg` / AppImage work on your platform, and that
nothing needs to be installed separately — no Qt6 libraries, no other
runtime — the app should just work after downloading. The emulation
itself is unchanged from the previous build: same features, same
limitations (see [Current limits](#current-limits) below). If the
package for your platform doesn't install/launch cleanly, that's exactly
the kind of feedback this release is looking for.

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

(The macOS `.dmg` is signed and notarized; the Windows installer is not
code-signed, so SmartScreen will warn on first launch — see the platform
notes below.)

## Downloads

Packaging-test build, tag
[`qt6-prototype-2026-09-14`](https://github.com/tinue/Calc-U-1600-Binary/releases/tag/qt6-prototype-2026-09-14).
Every package below is self-contained — no Qt6 install, no other runtime
required. Download, install/launch, done.

| Platform | Download | Notes |
|---|---|---|
| Windows (x86_64) | [Calc-U-1600-windows-x86_64.exe](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-14/Calc-U-1600-windows-x86_64.exe) | Installer — Qt runtime and the MSVC redistributable are bundled. Unsigned, so SmartScreen will warn ("More info" → "Run anyway"). |
| Linux (x86_64) | [Calc-U-1600-linux-x86_64.AppImage](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-14/Calc-U-1600-linux-x86_64.AppImage) | Self-contained AppImage — no Qt6 install needed. Download, `chmod +x Calc-U-1600-linux-x86_64.AppImage`, run. |
| Linux (arm64) | [Calc-U-1600-linux-aarch64.AppImage](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-14/Calc-U-1600-linux-aarch64.AppImage) | Same as above (e.g. Raspberry Pi OS 64-bit). |
| macOS (Apple Silicon) | [Calc-U-1600-mac-aarch64.dmg](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-14/Calc-U-1600-mac-aarch64.dmg) | Self-contained `.app` bundle in a `.dmg`, signed and notarized — no Qt6 install needed, no Gatekeeper warning. |

## Feedback

This is a feasibility test, not a release — if you try it, bug reports and
impressions are welcome, but please don't expect the missing features
above to show up here without a heads-up first.
