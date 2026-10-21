# HISTORY: CRT Studio Completed Work

Reverse-chronological, dated record of completed changes. Current and planned
steps belong to [TODO](TODO.md). Design, procedures, and measured acceptance
keep their own detailed records under [docs](docs/README.md).

Dates identify completion/documentation time; use a date span where appropriate.
Link commits and reproduction entry points when available, without inventing
commit IDs or test results. Older months may later move to `docs/history/`
with decisions, evidence, limitations, and original Git references preserved.

## 2026-10-21

### Make CLI prerequisites feature-specific and track shared contract adoption

Compared the supplied review with CRT `a23a173`, CLI `a76d8ad` and Studio
`d3793e3`. Replaced the ambiguous all-D0-D6 prerequisite with feature-level
conditions: SDK-only S0/UI PoCs and labeled fixtures may start early; live S3
build/run requires actual D5 workflow capabilities and applicable D6 job
contracts; D7 is formal approval of exercised combinations, not an S0 blocker.
JSON drafts are not deferred until D6.

Connected TODO, acceptance, index and agent guidance to the CLI-owned
`docs/compatibility.md` adoption record and producer-owned review procedure.
The original design baseline is unchanged; SDK/UI evidence, CLI evidence and
Studio UX evidence remain with their owners. No Studio implementation, native
GUI run, live CLI integration, automated CI check or release approval was
performed; all runtime acceptance remains Not run.
Documentation validation checks local links/anchors, English text, fences,
conflict markers and whitespace; external URLs were not network-validated.

## 2026-10-20

### Initialize Studio guidance and documentation ownership

Created AGENTS, the user-facing README, TODO, this history, and the documentation
index, local Studio design, development guide, and S0/S1 acceptance contract.
The design adopts the CRT cross-repository baseline at
`d21430ddeb59aea76cf6abd58c15a69f55cfda52` and records its origin; ongoing
Studio decisions now belong here. SDK and CLI contracts remain references to
their owners rather than copied engines or independently maintained designs.

TODO sets S0 external-consumer contracts/feasibility preparation as the current
focus and S1-S5 as ordered plans. The documents preserve CRT-native C++17,
public UI/graphics and SDK-only boundaries, CLI-first workflow delegation,
editing-data integrity, workspace trust, and distinct GUI/IME/debug acceptance.
Editor-engine adoption, a working CLI, native GUI execution, and release
availability are not assumed. Initial acceptance entries are Not run.

Documentation checks cover English text, links/anchors, fences, whitespace,
and queue structure. No Studio source/build implementation, runtime replay,
commit/push, public release, or changes to neighboring repositories are claimed
by this documentation initialization.
