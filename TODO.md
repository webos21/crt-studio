# TODO: CRT Studio Work Queue

This file owns concise In Progress and Planned work. Architecture and stage
order belong to [the Studio design](docs/design/crt_studio.md), procedures to
the [development guide](docs/guides/development.md), and measured results to
[acceptance](docs/acceptance/bootstrap_acceptance.md). Completed work moves
to [HISTORY](HISTORY.md).

## Notice

- Follow [AGENTS](AGENTS.md); advance one bounded, authorized increment at a
  time. A roadmap entry is not authorization to implement every stage.
- In Progress identifies the current focus, not completed implementation.
  Move completed details to HISTORY/acceptance and remove completed queue items.
- Keep SDK/ABI and CLI environment/port/workflow evidence with their original
  owners; link it rather than duplicating status matrices here.
- Do not copy SDK installers or recipe engines into Studio when a CLI contract
  is unavailable. Record the gap and coordinate the prerequisite.
- Keep README user-facing. Do not create/update STATUS as a routine step;
  update it only when explicitly requested.
- A model/protocol fixture, cross compile, skip, or headless CI result is not
  native GUI/IME/debugger acceptance or release authorization.

## In Progress

### S0 - External Consumer Contract and Feasibility Preparation

Current focus: design and prerequisite definition. No Studio implementation,
build/test entry point, native window, or live CLI integration exists yet.
Use [S0/S1 acceptance](docs/acceptance/bootstrap_acceptance.md).

- [ ] Identify actual immutable SDK candidates, public UI/import/toolchain
  paths, host/target identities, and minimum runtime closure; evaluate `05-ui`
  without requiring WebKit for the initial window.
- [ ] Inventory real CLI availability/version/capabilities and define the
  adapter/schema boundary. Separate protocol fixtures from live integration.
  Record adopted inputs in `crt-cli: docs/compatibility.md`; SDK-only S0 does
  not wait for D7 or claim approval of a runnable three-product combination.
- [ ] Audit public input/focus/drawing/layout/IME capabilities; record actual
  producer gaps and high-risk feasibility cases instead of assuming gaps.
- [ ] Define the minimal window/input/shutdown consumer, lifecycle/ownership,
  runtime audit, and initial configuration/test entry points.
- [ ] After prerequisite review, implement and validate that minimal consumer
  through the public installed SDK and document real build/run commands.

## Planned

Follow [S0-S5 dependency order](docs/design/crt_studio.md#5-staged-goals).
CLI-first contracts remain prerequisites; scoped UI/IME/editor PoCs may proceed
without pretending that unfinished CLI workflows already work.

### S1 - Native Workbench

- [ ] Add explorer/editor/build placeholders, menus/settings/layout and focus,
  resize, cursor, High-DPI, and toolkit-lifetime handling.
- [ ] Validate native IME composition/caret/candidate placement/commit/cancel,
  public editor-surface feasibility, and three-host GUI behavior.

### S2 - Editor and Language Services

- [ ] Evaluate editor engines through license/build/adapter PoCs before
  adoption; implement document ownership, undo/redo, save, and recovery.
- [ ] Add syntax/LSP with validated native tools, Unicode editing, external
  changes, and failure-safe document handling.

### S3 - CLI Build and Run Integration

- [ ] Present SDK/port/project operations through the compatible CLI/JSON
  contract, with exact locks/plans, diagnostics, progress, and cancellation.
  Gate live build/run on implemented D5 commands and applicable D6 job contracts
  ([feature prerequisites](docs/design/crt_studio.md#5-staged-goals)), not all of D7.
- [ ] Verify parity with CLI outcomes, workspace trust, error recovery, and
  owned-process teardown; do not create a duplicate workflow engine.

### S4 - Debugging

- [ ] Integrate validated native debugger/DAP tools for breakpoints, stepping,
  threads/stacks, process lifecycle, and restart/recovery.
- [ ] Validate CRT ABI/startup behavior, including Windows DWARF/emutls;
  debugger availability alone is not passing debug acceptance.

### S5 - Preview, Packaging, and Self-development

- [ ] Package Studio and required runtime/CLI dependencies for execution
  without development SDK/build roots; preserve notices/source obligations.
- [ ] Add optional preview/AI integration when needed and prove Studio's
  independent-workspace self-build/debug workflow.

### Deferred Scope

Plugin marketplaces, new daemon/RPC protocols, full LVGL exposure, unverified
terminal/PTY behavior, additional architectures, and further Web features need
separate scope/evidence. Do not make them prerequisites for the first window.
