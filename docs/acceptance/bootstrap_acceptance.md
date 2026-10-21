# S0/S1 Bootstrap Acceptance

This document owns initial Studio consumer/workbench acceptance criteria and
execution evidence. Architecture and stage order belong to the
[Studio design](../design/crt_studio.md), procedures to the
[development guide](../guides/development.md), and current work to
[TODO](../../TODO.md).

## Scope and Evidence Boundaries

S0 validates the public installed SDK consumer and minimal window/input/
shutdown boundary. S1 adds the workbench and native UI/IME feasibility.
These are future requirements, not claims of implemented or passing features.

Keep five kinds of evidence separate:

1. Model/protocol fixture tests without a live GUI or CLI.
2. SDK-only compile/link and dependency audits.
3. Actual native window/input/workbench/IME execution.
4. Live CLI workflow integration, with a real compatible executable.
5. Packaged Studio execution and actual editor/debugger behavior in later stages.

A fixture pass is not live CLI integration, a headless render is not native
GUI acceptance, and cross compilation is not execution. Missing public APIs
or CLI contracts are recorded as prerequisite gaps, not implemented here as
private includes or duplicate installers/engines.

An SDK-only S0 result may be recorded before CLI D7; specify its accepted scope
and keep S0-05 fixture evidence distinct from unavailable live integration.
S3 build/run later requires the actual D5 workflow capabilities and applicable
D6 job contracts listed in the [feature prerequisites](../design/crt_studio.md#5-staged-goals).
D7 approves an exercised combination, not permission to start a window PoC.
Link exact adopted contracts and original case evidence from
`crt-cli: docs/compatibility.md`; do not infer compatibility from matching
design baseline commits or proposed v1 names.

## S0 - External Consumer

| ID | Required evidence |
| --- | --- |
| S0-01 Inputs | Exact SDK/tool/CLI identities or explicitly unavailable prerequisites; host/target separate; actual public headers/import/toolchain and runtime capabilities inventoried |
| S0-02 Build boundary | Fresh CRT-native consumer configure/compile/link using installed SDK wrappers/toolchain; no CRT/CLI source or build-tree linkage, private LVGL headers, or substituted host C/C++ runtimes |
| S0-03 Native window/input | Actual public CRT window, visible presentation, keyboard/mouse delivery, focus, resize, and clean shutdown; synthetic/model-only checks labeled separately |
| S0-04 ABI/runtime closure | ELF/Mach-O/PE checks and mapped-runtime evidence as applicable; allowed OS boundaries declared; minimal UI consumer does not acquire WebKit unnecessarily |
| S0-05 CLI adapter contract | Schema/version/capability handling, structured diagnostics vs logs and failure states; fixtures identified explicitly, unavailable live CLI integration left unaccepted |
| S0-06 Independence/lifecycle | Real spaced/Unicode paths; producer build roots hidden/unavailable during external consumer build/run; repeated create/destroy and owned-process cleanup within declared bounds |

## S1 - Workbench and Native UI Feasibility

| ID | Required evidence |
| --- | --- |
| S1-01 Workbench | Explorer/editor/build placeholders, menus/settings/layout and public toolkit ownership; no IDE-specific policy moved into CRT |
| S1-02 Interaction | Focus/key/shortcut, clipboard as supported, cursor, scale/clipping, High-DPI and resize behavior; actual unsupported cases recorded |
| S1-03 IME | Native Korean composition ranges, caret/candidate-window position, focus, commit/cancel on each applicable native OS; not just UTF-8 commit |
| S1-04 Editor surface | Public drawing/text/input feasibility and engine PoC evidence; no assumed Scintilla adoption or completed port |
| S1-05 Trust/failure recovery | Opening an untrusted workspace does not execute scripts; missing CLI/tool/schema failures are actionable; jobs are bounded/cancelled/cleaned up without killing unrelated processes |

Use disposable test documents and controlled fixtures. Agree on repetition
counts/timeouts before long lifecycle runs. Preserve failures rather than
retrying until a flaky case appears green. Do not change global PATH, registry,
Developer Mode, or security settings to manufacture negative cases.

S1 editor-surface feasibility does not close S2 document/undo/save/recovery,
S3 live build/run parity, S4 debugging, or S5 packaging/self-development.
Those stages need their own scoped evidence as implementation progresses.

## Evidence Record Format

For every executed case record:

1. Case ID/date and Studio revision or clearly identified dirty source snapshot.
2. Host OS/architecture, target tuple, native/cross/runner classification, and
   relevant display/scale/input-method details.
3. SDK/CLI/schema/toolchain/host-tool identities and original producer evidence
   links. Document which fixtures replace unavailable live prerequisites.
4. Exact configure/build/run/test command/argv, sanitized environment, real
   paths, timeout/repeat counts, and expected behavior.
5. Actual result, exit/error/diagnostics, bounded logs and artifact references;
   GUI frames/input observations or screenshots where needed to prove behavior.
6. Dependency/runtime mappings, input inventories and source/build independence
   checks where applicable; remaining owned processes and restoration state.
7. Unsupported cases, skipped variants, limitations, and linked producer/CLI
   issue/commit. Do not copy another repository's measured result as Studio's.

Use distinct outcomes: **Pass**, **Fail**, **Not run**, **Skipped** (with reason),
or **Compile/package only**. An absent prerequisite is Not run with the gap
identified. A successful fixture remains fixture evidence even if all assertions
pass. Keep failed attempts separate from accepted artifact combinations.
Redact tokens, private keys, personal workspace data, and sensitive paths as
needed without hiding the facts required to reproduce a failure.

## Initial Evidence Ledger

No Studio product implementation or execution has been performed at contract
initialization. Only documentation has been authored and checked.

| Native host/target | S0 | S1 | Live CLI workflow | Evidence |
| --- | --- | --- | --- | --- |
| Windows/x64 | Not run | Not run | Not run | No Studio build/executable yet |
| Linux/x86_64 | Not run | Not run | Not run | No Studio build/executable yet |
| macOS/arm64 | Not run | Not run | Not run | No Studio build/executable yet |

Update from actual runs with case records and limitations. WSL/headless checks
must be labeled and do not replace native GUI/IME/device acceptance. Additional
architectures or cross pairs require separate evidence. Documentation checks
belong in HISTORY and do not turn this ledger green.

Closing S0/S1 does not authorize a public preview/release or prove editor,
debugger, packaging, or independent self-development. SDK/CLI support and
source/license/security obligations remain separate prerequisites.
