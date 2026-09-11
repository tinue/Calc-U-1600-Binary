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

- All three models (PC-1500, PC-1500A, PC-1600): faceplate art, resizable
  window, model switching, Reset / ALL RESET.
- A live-rendering LCD (dot matrix + status indicators) and clickable
  on-screen keys.
- Full host-keyboard typing support, including SHIFT-tapped symbols and
  the PC-1600's digit-row second legend (`' [ ] `` { } \ ~ _ | ^`).

## What's not in this prototype

Memory modules, presets/BASIC loading, plotters, the debugger panel,
settings persistence, and (on macOS/Linux) any packaging/signing — those
two platforms' builds are plain executables for people comfortable running
one from a terminal, not double-click-ready apps.

## Downloads

Latest build (commit
[`bd6c0db`](https://github.com/tinue/Calc-U-1600/commit/bd6c0dbb1c0cbdfc3a497f51f0d821865c4931c0)
on the `qt6-prototype` branch):

| Platform | Download | Notes |
|---|---|---|
| Windows (x86_64) | [Calc-U-1600-Qt6-windows-x86_64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11/Calc-U-1600-Qt6-windows-x86_64.zip) | Self-contained — Qt runtime and the MSVC redistributable are bundled. Unzip anywhere and run `CalcU1600Qt.exe`. |
| Linux (x86_64) | [Calc-U-1600-Qt6-linux-x86_64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11/Calc-U-1600-Qt6-linux-x86_64.zip) | Requires Qt6 already installed (`qt6-base-dev` + `qt6-wayland` on a Wayland desktop, via apt or your distro's equivalent). Unzip, `chmod +x CalcU1600Qt`, run. |
| Linux (arm64) | [Calc-U-1600-Qt6-linux-arm64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11/Calc-U-1600-Qt6-linux-arm64.zip) | Same requirements as above (e.g. Raspberry Pi OS 64-bit). |
| macOS (Apple Silicon) | [Calc-U-1600-Qt6-macos-arm64.zip](https://github.com/tinue/Calc-U-1600-Binary/releases/download/qt6-prototype-2026-09-11/Calc-U-1600-Qt6-macos-arm64.zip) | Requires Qt6 already installed (`brew install qt`). It's a bare executable, not a `.app` — unzip, `chmod +x CalcU1600Qt`, then `xattr -d com.apple.quarantine CalcU1600Qt` (unsigned, so Gatekeeper blocks it otherwise) and run from a terminal. |

All builds come from the same commit; see the
[GitHub Actions run](https://github.com/tinue/Calc-U-1600/actions/runs/34580642970)
that produced them.

## Feedback

This is a feasibility test, not a release — if you try it, bug reports and
impressions are welcome, but please don't expect the missing features
above to show up here without a heads-up first.
