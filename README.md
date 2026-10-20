# CRT Studio

CRT Studio is a planned CRT-native IDE for developing C and C++ applications
on Linux, Windows, and macOS. It is intended to make
[CRT](https://github.com/webos21/crt) application development approachable
without manually configuring startup objects, sysroots, special compiler/link
flags, or runtime search paths.

Studio provides the visual workspace; CRT-CLI provides the development
workflow. The goal is to create, edit, build, run, debug, and package CRT
applications through the same reproducible SDK and project contracts used by
the command line, CI, and automation.

## Project Maturity

This repository currently contains design and development documentation only.
There is no implemented IDE, editor, build configuration, executable, installer,
or published Studio package. The capabilities below describe the target
product, not available features or a completed platform support matrix.

## Intended Capabilities

- A native project workbench with explorer, editor, build output, and settings.
- Safe document editing, Unicode/IME input, undo/redo, save, and recovery.
- SDK selection, port-library integration, and build/run/test/package controls
  delegated to the separate [CRT-CLI](https://github.com/webos21/crt-cli).
- Code intelligence through LSP and debugging through validated native
  debugger/DAP integration.
- Optional documentation/preview through CRT's public WebView API.
- Eventually, development of Studio itself from an independent workspace.

Studio targets CRT-native C++17 and public CRT UI/graphics APIs. LVGL is private
to CRT; Studio is not a second UI toolkit or package manager. An editor engine
has not been selected. The first window/workbench should not require the
entire WebKit runtime merely to start.

## Platform Direction

Initial native validation targets are Windows/x64, Linux/x86_64, and
macOS/arm64. GUI, IME, debugger, and packaging behavior will need actual native
evidence. Windows build/source-stage hosts require Developer Mode and real
symlinks; this is not a claim that every eventual end-user installation needs
Developer Mode. Final installation requirements remain to be validated.

## Learn More and Contribute

- [Documentation](docs/README.md): design, development, and acceptance index.
- [Development guide](docs/guides/development.md): the initial contract and
  SDK-only consumer preparation; no executable quick start exists yet.
- [TODO](TODO.md): In Progress and Planned work.
- [HISTORY](HISTORY.md): dated completed work.
- [AGENTS.md](AGENTS.md): repository development rules.

The early focus is a correct external SDK consumer and clear CLI/UI boundaries,
not a full IDE implementation. Preserve user data and avoid producer-private
dependencies when contributing.
