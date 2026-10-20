# Development and Bootstrap Guide

This is the initial Studio development process, not an executable quick start.
The repository currently has documentation only; there are no implemented
CMake targets, presets, test runner, IDE binary, or installer to invoke.

## Before Making Changes

1. Read [AGENTS](../../AGENTS.md), [TODO](../../TODO.md),
   [HISTORY](../../HISTORY.md), and the [Studio design](../design/crt_studio.md).
2. Inspect git status and preserve unrelated user changes. Select one bounded,
   authorized increment; a work queue does not authorize the entire roadmap.
3. Read the applicable [acceptance contract](../acceptance/bootstrap_acceptance.md).
   Record missing prerequisites rather than inventing an installed SDK/CLI.

## S0 Input and Capability Inventory

Before a first native build, identify actual immutable inputs:

- Public installed SDK stage, source/build/content identity, target tuple,
  toolchain/wrappers/imports, public UI/graphics headers, and runtime closure.
  Evaluate `05-ui` without making WebKit an empty-window prerequisite.
- Execution host, approved external LLVM/LLD, CMake/Ninja and OS/vendor SDK,
  required host tools, and Windows Developer Mode/symlink prerequisites.
- Selected CLI executable/version/content identity and actual supported
  schema/capabilities, or an explicitly recorded unavailable prerequisite.
- Current public UI focus/input/drawing/layout/IME behavior and reproducible
  producer gaps. A design checklist is not evidence that every API is missing.

The pinned CRT design revision is not a downloaded SDK identity. Sibling
checkouts may provide context, not private headers/libraries or build outputs.
Do not change CRT or CRT-CLI without authorization covering that repository.

## Consumer Bootstrap and CLI-first Ordering

Follow [S0-S5](../design/crt_studio.md#5-staged-goals). Define the minimal
window/input/shutdown consumer and SDK-only build/test entry points before
growing the workbench. Use the SDK's actual wrappers and CMake toolchain;
do not manually reconstruct startup/link flags or expose private LVGL APIs.

A scoped SDK-only UI/IME/editor PoC may be considered while CLI prerequisites
are still being developed. It does not prove live CLI integration. Clearly
label protocol fixtures and record unavailable command/schema capabilities;
do not implement a substitute SDK manager or port engine inside Studio.

Add actual configure/build/run/test commands here once those entry points
exist and are verified. Fresh configuration is required for build-wiring
changes. Do not copy commands from producer presets or advertise planned
commands as working Studio instructions.

## UI, Editor, and Debug Feasibility

Separate headless/model checks from actual native window/input behavior.
Exercise focus, resize, scale/clipping, High-DPI, ownership, and clean shutdown
through public CRT APIs. IME needs native composition, caret/candidate-window
placement, commit/cancel, and focus evidence; UTF-8 commit alone is insufficient.

Evaluate editor engines before adoption, with license/build/adapter evidence.
Studio owns document data, undo/save/recovery; do not risk user files during
PoCs. Use dedicated fixtures and preserve unsaved edits and original content.

Approved clangd/debugger/DAP tools may initially be native host processes;
target apps remain CRT-built. Debugger presence or headless CI success does
not validate CRT breakpoints/stepping/threads/stacks, Windows DWARF/emutls,
or restart/teardown. Those require later actual debug acceptance.

## Verification and Documentation

Use [S0/S1 acceptance](../acceptance/bootstrap_acceptance.md) for identities,
commands, evidence classification, and native GUI requirements. Record
host/target and exact CLI/SDK/tool artifacts. Test real paths containing spaces
and Unicode and remove/hide producer build inputs for external-consumer checks.
Diagnose missing Developer Mode without toggling global security settings.

Opening a workspace must not automatically run scripts. Show trust/commands,
use explicit argv, track owned jobs, and bound timeouts/cancellation. Hidden
automation children are distinct from explicitly requested GUI validation.
Do not terminate unrelated processes or hide failures with retries.

Documentation-only work requires links/anchors, English text, fences, and
formatting checks, not a full CRT/WebKit rebuild. Model/protocol fixtures,
native GUI/IME, live CLI workflows, and packaged app execution need separate
evidence. Put completed outcomes in HISTORY, active steps in TODO, and original
measurements in acceptance. Update STATUS only when explicitly requested.

Commit/push, publication, neighboring-repository changes, global environment
changes, and destructive cleanup require authorization covering those actions.
No preview/release permission follows from documenting a development snapshot.
