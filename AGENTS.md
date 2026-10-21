# Agent Development Guidelines

## Mission and Scope

Build CRT Studio, a CRT-native C++17 IDE for Linux, Windows, and macOS.
Its purpose is to make CRT application development accessible without manual
startup/sysroot/compiler/link/runtime configuration, not to create another
SDK manager or port engine inside a GUI.

Studio owns the workbench, editor/document model, project UX, LSP/DAP clients,
and presentation of CLI workflows. CRT owns the runtime/PAL and public
graphics/UI/Web APIs. CRT-CLI owns SDK/host-tool installation, port resolution
and builds, locks, and project build/run/test/package execution.

The CLI-first sequence is deliberate. Studio is a thin workflow frontend, not
a replacement for the CLI. Do not start a plugin marketplace, new GUI toolkit,
full LLVM port, or competing package manager as part of initial bootstrap.

## Starting Work and Design References

Read [README](README.md), [TODO](TODO.md), [HISTORY](HISTORY.md), and the
[documentation index](docs/README.md). The [local Studio design](docs/design/crt_studio.md)
owns ongoing Studio decisions; the [development guide](docs/guides/development.md)
owns procedures and [S0/S1 acceptance](docs/acceptance/bootstrap_acceptance.md)
owns validation criteria/evidence.

The initial cross-repository baseline is CRT revision
`d21430ddeb59aea76cf6abd58c15a69f55cfda52`:

- [Original Studio design](https://github.com/webos21/crt/blob/d21430ddeb59aea76cf6abd58c15a69f55cfda52/docs/design/crt_studio.md).
- [SDK Development Contract](https://github.com/webos21/crt/blob/d21430ddeb59aea76cf6abd58c15a69f55cfda52/docs/design/sdk_development_contract.md).
- [CLI joint development contract](https://github.com/webos21/crt/blob/d21430ddeb59aea76cf6abd58c15a69f55cfda52/docs/design/crt_cli.md).

These links pin the adopted design, not a released SDK/CLI combination.
Coordinate later producer/CLI contract changes explicitly. Do not maintain
independently edited copies of SDK or CLI designs here. Adjacent checkouts may
provide context, but they are not application build inputs.

For shared owner/version/capability changes, use the CLI-owned adoption record
`crt-cli: docs/compatibility.md` and its Shared-change Review section in the
[CLI repository](https://github.com/webos21/crt-cli). Review immutable baseline
references, proposed vs implemented commands, and TODO-to-acceptance links;
coordinate producer-owned contracts before updating consumer locks. Keep the
original design provenance separate from actually tested combinations. D7
formal approval does not block SDK-only S0; live features require their actual
command/schema capabilities and original evidence.

Inspect git status and applicable instructions before editing. Preserve user
changes. During initial setup, do not invent existing sources, presets, test
commands, executables, screenshots, or completed acceptance results. A design
or work queue does not authorize implementing every planned stage.

## SDK-only Native Build Boundary

- Use C++17, CMake, Ninja by default, and CTest for project-owned tests.
- Consume public installed CRT SDK artifacts with exact source/build/content
  identities. Do not include CRT source/private headers, vendor the producer,
  reference sibling build outputs, or use `add_subdirectory(../crt)`.
- Delegate startup, freestanding flags, sysroot, C++ runtime, and link policy
  to the SDK wrappers and `crt-toolchain.cmake`. Do not reconstruct them in
  Studio or project templates.
- Use CRT libc/PAL and imported libc++/libc++abi/libunwind, not substitute host
  standard runtimes. Preserve Windows CRT DWARF/Itanium exception policy;
  SDK-declared OS/PAL boundaries remain allowed.
- Start by evaluating a public UI-only `05-ui` consumer. Determine the minimum
  SDK/capabilities from actual link/deploy requirements; do not require WebKit
  just to display an empty workbench.
- Use public `crtui`/`crtgfx` APIs. LVGL is private to CRT; do not include LVGL
  types/private headers or expose private Skia/WebKit objects across APIs/IPC.
- Detect a missing SDK/UI/PAL capability with a small reproducer and request
  the producer-side contract/fix. Do not silently patch a sibling repository,
  expose host headers/libraries, or redesign CRT public APIs inside Studio.

CRT runtime/SDK production must not depend on Studio. Self-development means
building Studio sources in an independent workspace with a pinned SDK/CLI,
not a circular source-tree build.

## CLI Integration and Process Ownership

Use an explicitly selected CLI executable and versioned command/JSON contract.
Check schema/capabilities and expose CLI/SDK identities, project locks, plans,
and job state in the UI. Do not select an arbitrary `crt` from global PATH or
silently follow a channel/main branch.

Delegate SDK/port installation, lock changes, configure/build/run/test/package,
and environment selection to the CLI. Do not embed another downloader,
resolver, recipe engine, or environment manager. If a CLI capability is not
available, document the gap or use clearly labeled protocol fixtures; do not
report fixture success as live integration or invent successful commands.

Use CLI plus JSON as the initial boundary. Do not add an internal shared C++
ABI, daemon, or RPC service without a demonstrated need. Keep structured
results separate from child/application stdout/stderr and preserve actionable
file/line/column/tool diagnostics.

Execute argv arrays instead of shell interpolation. Jobs need bounded timeouts,
cancellation, ownership, and lifecycle reporting. On shutdown, clean up only
owned jobs and workers; never use global executable-name kills or unbounded
retries. Windows background build/diagnostic children are hidden by default;
open an interactive terminal only when requested. Distinguish automatic jobs
from explicitly requested native GUI validation.

Do not invent process-group cancellation or PTY/ConPTY capabilities before
CRT/PAL support is verified. A build-log panel does not imply terminal support.
Do not modify global PATH, shell profiles, registry, or security settings.

## User Data, Editing, and Workspace Trust

Editing-data integrity takes priority over cosmetic UI features. Studio owns
document buffers, undo/redo, dirty state, save, external-change handling, and
crash recovery. Test Unicode, large/partial files, save failures, and recovery
as those features are introduced. Never overwrite user files or discard
unsaved edits silently.

Opening a workspace, recipe, document, or project does not authorize executing
it. Show commands/trust origins and use explicit workspace trust and consent.
Do not automatically build/install/run arbitrary workspace content. Redact
tokens, passwords, private keys, and sensitive environment values from logs,
diagnostics, project metadata, and reports.

Keep IDE-specific docking policy, editor state, breakpoint models, and project
UX here. Add only genuinely reusable primitives to CRT through coordinated,
authorized producer changes. Do not expose the entire LVGL widget set merely
because a Studio feature needs a new interaction.

## UI, Editor, and Debugger Decisions

Audit current public capabilities instead of declaring every design checklist
item missing. Validate focus/keyboard/shortcuts, clipboard, scale/clipping,
cursor/High-DPI, layout primitives, and lifecycle at their applicable stages.

IME acceptance includes composition ranges, caret/candidate-window placement,
focus, commit, and cancel on actual native Windows, Linux, and macOS input
paths. A UTF-8 commit event or synthetic fixture alone is not full IME proof.

Scintilla and other editor engines are evaluation candidates, not selected or
ported dependencies. Review license fit, CRT-only builds, and public
drawing/input adapter requirements before adoption. Do not hide CRT failures
by arbitrary upstream patches or native-toolkit replacement.

clangd, LLDB/DAP, CMake/Ninja, and other declared generators may initially be
approved native host tools. Track executable/version identities separately
from CRT target applications. Tool presence alone does not prove CRT debugging:
validate breakpoints, stepping, stack/thread inspection, lifecycle, and Windows
DWARF/emutls/startup behavior through actual debug acceptance.

WebView is optional for documentation/preview. Use public `crtweb` APIs when
needed and preserve worker/resource/runtime ownership. Do not expose private
WebKit/Skia objects or assume that WebView implies a security sandbox.

## Implementation and Verification Sequence

Follow S0-S5 in the local design: external SDK consumer, workbench, editor,
CLI build/run integration, debugging, then preview/packaging/self-development.
Respect CLI prerequisite contracts. High-risk UI/IME/editor feasibility work
may proceed in parallel when scoped, without inventing a working CLI or
bypassing public APIs.

For each authorized increment, record a small scope in TODO, define the
contract and regression, implement it, validate applicable native behavior,
and document evidence before advancing. Do not expand a documentation request
into implementation. Use fresh CMake configuration for wiring changes and
record real build/test commands only after they exist.

Separate headless/model fixtures, public API tests, native GUI/IME evidence,
CLI integration, and packaging/debugger acceptance. Initial native replay
targets are Windows/x64, Linux/x86_64, and macOS/arm64. Additional architectures
and cross pairs need explicit evidence. Do not substitute WSL/headless output
for native GUI/device acceptance or label cross compilation as execution.

Exercise real paths with spaces and Unicode, SDK/build-tree removal or hiding,
private-runtime mapping, focus/resize/High-DPI, failure recovery, clean teardown,
and owned-process leftovers as applicable. Windows build/source-stage hosts
require Developer Mode and real symlinks; diagnose absence without changing
settings or substituting MSYS marker links, shortcuts, or deep copies.

Documentation-only changes need link/anchor, formatting, and consistency
checks, not a full CRT/WebKit rebuild. A passing CI fixture or development SDK
does not authorize a release or prove native GUI/editor/debugger acceptance.

## Documentation and Change Discipline

Write new documentation and code comments in English. Root README is the
user-facing introduction; TODO owns concise In Progress/Planned work; HISTORY
owns dated completed work. Design, procedures, and measured acceptance belong
to their respective `docs/` owners. Update STATUS only when explicitly asked.
Do not copy completion matrices into every document.

Studio acceptance owns UX/editor/CLI-integration results. Link original CRT
ABI/SDK and CLI environment/port/project evidence instead of duplicating it.
Record exact source/artifact/tool identities, commands, host/target, outcomes,
and limitations. Retain failed identities separately and use bounded logs
without secrets. Keep generated build/download/cache/binary outputs outside
tracked source.

Do not modify neighboring repositories, create/push commits, publish packages,
or change release/security settings without authorization covering that action.
Coordinate shared changes through linked producer/CLI/Studio revisions:
validate/promote the producer artifact first, then update consumer locks.
Preserve previous known-good combinations and do not overwrite artifact
identities or conceal failures through retries.
