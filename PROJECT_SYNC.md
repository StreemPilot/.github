# GitHub and Linear project synchronization

Last updated: 2026-08-05

## Canonical mapping

- GitHub organization: `StreemPilot`
- GitHub project input / release-train issue: [`.github#2`](https://github.com/StreemPilot/.github/issues/2)
- GitHub Actions/runner blocker: [`.github#1`](https://github.com/StreemPilot/.github/issues/1)
- Linear project: `github.com/streempilot`
- Linear project ID: `3f5bd157-4424-42cc-94d0-0bed993cdc1d`
- Linear foundation issue: `DEN-896`
- Linear API issue: `DEN-900`
- Linear web issue: `DEN-901`
- Linear rooms/control issue: `DEN-903`
- Linear destinations issue: `DEN-907`
- Linear sync issue: `DEN-909`
- Linear automation issue: `DEN-913`
- Linear E2E/release issue: `DEN-918`

## Source-of-truth responsibilities

GitHub owns executable code, pull requests, exact commit SHAs, review threads, checks, release artifacts, deployment declarations, and repository-local issues.

Linear owns cross-repository product planning, dependencies, priorities, milestones, release readiness, and polished project documentation.

Neither system should claim evidence held only by the other. Linear status updates link exact GitHub PRs/commits; GitHub issues link the relevant Linear IDs.

## Suggested GitHub Project fields

| Field | Values / rule |
| --- | --- |
| Status | Backlog, Ready, In progress, In review, Blocked, Done |
| Workstream | Foundation, Contracts, API, Studio, Media, Destinations, Recording, Sync, Automation, E2E, Infrastructure |
| Repository | exact `owner/repository` |
| Linear ID | one canonical issue identifier |
| Priority | Urgent, High, Medium, Low |
| Release gate | None, Contract, Security, CI, E2E, Deployment, Operations |
| Blocked by | issue or PR URL |
| Target | milestone/release name |

## Project item policy

1. Use one organization-level tracking issue for a cross-repository deliverable.
2. Link implementation PRs and repository-local issues from that item.
3. Do not create duplicate GitHub issues when a canonical repository issue already exists.
4. Keep drafts blocked when dependency publication, runner execution, review, or deployment evidence is incomplete.
5. Close obsolete PRs with an explicit superseding PR/commit and preservation rationale.
6. Mark a project item Done only after the merge/deployment or documented cancellation—not merely after a branch was pushed.

## Current August 5 execution ledger

### Merged

| Repository | PR | Result |
| --- | ---: | --- |
| `sp-api` | #3 | explicit local bootstrap transport contract; merge `9c65c4a2232e9bebf46a4f1f09f3397ac7c026c3` |
| `sp-web-leptos` | #7 | fail-closed realtime hardening; merge `144fb53b8c0391524952ed9e68b68ac2e6a08c02` |
| `sp-web-dioxus` | #7 | fail-closed realtime hardening; merge `e39cb8589ad65bcc55d3936f2e2792c93718f521` |
| `sp-cli` (`dev`) | #6 | removed unresolved `sp-libs` package coordinate; merge `8bd54fc48bda37c2381ce326cf1858e89a4843c5` |

### Closed as superseded

- `sp-sync#3` is superseded by merged `sp-sync#4` (`f755960eac6de9261c99c9840bbedd9e7004f6d1`) and would recreate a second root Rust package.

### Blocked or draft

- `sp-web-mash#12`: production/alternate-surface parity train; exact-head execution blocked by the Actions gate and now needs scope reconciliation after standalone Leptos/Dioxus merges.
- `streempilot-api-server.rs#22`: authenticated live-control WebSocket work in the mature API train; compare with `sp-api` before consolidation.
- `streempilot-monorepo#16`: reviewed media-router starter; repository provisioning and executable CI evidence remain incomplete.
- `streempilot-monorepo#10` and `streempilot-clients#6`: create/publish `sp-libs` and converge the client identity.
- `.github#1`: restore hosted Actions and certify ARC fallback.

## Projects-v2 connector limitation

The currently connected GitHub app exposes repositories, issues, pull requests, reviews, checks, artifacts, and source writes but not Projects-v2 field/item mutations. Therefore:

- `.github#2` is the stable organization-level item to add to the project;
- repository issues and PRs are linked from it;
- Linear remains the active mirrored planning authority;
- no claim is made that a Projects-v2 board field was mutated until a Projects-capable GitHub credential/tool is connected.

If an organization project has auto-add rules for `StreemPilot/.github` issues, issues #1 and #2 may be added automatically; verify that state in the GitHub UI or with Projects-capable CLI/API access.
