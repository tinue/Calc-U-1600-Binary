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

## Current limits

Just two, for now: **no memory modules** and **no plotter**. Everything
else — the machine you're actually typing on — is the real thing.

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
