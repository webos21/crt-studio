# Documentation

Start with the [project introduction](../README.md),
[Studio design](design/crt_studio.md), and
[development guide](guides/development.md).
[AGENTS](../AGENTS.md) defines development rules;
[TODO](../TODO.md) owns the active/planned queue and
[HISTORY](../HISTORY.md) records dated completed work.

## Architecture and Policy

- [CRT Studio: CLI-backed Native IDE](design/crt_studio.md): ownership,
  SDK/CLI boundaries, UI/editor/debug decisions, and S0-S5 dependency order.
  This repository owns subsequent Studio-specific design decisions.

The initial cross-repository baseline stays pinned in CRT:

- [SDK Development Contract](https://github.com/webos21/crt/blob/d21430ddeb59aea76cf6abd58c15a69f55cfda52/docs/design/sdk_development_contract.md).
- [CLI integration and joint sequence](https://github.com/webos21/crt/blob/d21430ddeb59aea76cf6abd58c15a69f55cfda52/docs/design/crt_cli.md).

These are design references, not a claim that every described SDK/CLI feature
is implemented or released. Coordinate later contract changes with their
owning repositories rather than maintaining independent copies here.

## Development and Usage Guides

- [Development and Bootstrap Guide](guides/development.md): initial SDK-only
  consumer preparation and CLI/UI feasibility work. There is no executable
  installation/build quick start yet.

## Acceptance Contracts and Evidence

- [S0/S1 Bootstrap Acceptance](acceptance/bootstrap_acceptance.md): external
  consumer, native window/input/lifetime, workbench/IME, and evidence rules.
  Authored criteria and protocol fixtures are not passing runtime results.

## Document Ownership

| Document | Owns | Does not own |
| --- | --- | --- |
| Root README | User-facing purpose, maturity, navigation | Detailed work queue or per-host measurements |
| AGENTS | Development rules, ownership, safety boundaries | Running implementation status |
| TODO | Concise In Progress and Planned steps | Completed investigation logs |
| HISTORY | Dated completed changes, reasons, evidence links | Future execution order |
| `docs/design/` | Contracts, architecture, rationale, stage dependencies | Duplicate completion checklists |
| `docs/guides/` | Real setup/build/use/reproduction procedures | Unimplemented commands presented as available |
| `docs/acceptance/` | Validation requirements, actual outcomes, limitations | General project introduction |

Write documentation in English. Update the owner and link to it instead of
repeating the same state across README/TODO/HISTORY. Completed details move
from TODO to HISTORY and applicable acceptance; retain failed attempts
separately from accepted artifact identities.

Keep CRT API/ABI/SDK and CLI environment/port/project measurements with their
owners. Studio owns native UX/editor/debug and end-to-end CLI integration
results, linking exact prerequisite identities and original evidence.

Do not routinely create/update STATUS. Add reference, release, or monthly
history directories when real content needs them, not as empty placeholders.
Future history archives must retain decisions, reproduction entry points,
limitations, and original Git references.
