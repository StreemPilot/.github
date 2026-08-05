# StreemPilot Rust server modularization and provisioning ledger

This document is the StreemPilot organization view of the cross-organization program tracked by Linear [DEN-1682](https://linear.app/denman/issue/DEN-1682) and [DEN-1757](https://linear.app/denman/issue/DEN-1757).

## Architecture contract

Every Rust service binary keeps `main.rs` as process wiring only. Independently testable modules own configuration, observability initialization, dependency construction, routes or MCP tools, transport, bounded validation, security middleware, background-task lifecycle, and product handlers.

Product policy stays in the product repository. A shared runtime crate is introduced only after two merged consumers demonstrate the same stable contract and compatibility tests. MCP services remain read-only visibility layers and never become alternate persistence paths. Media services keep signaling, media, recording, compositing, provider credentials, and control-plane authority in explicit separate planes.

## Wave 1 implementation evidence

| Repository | Boundary | Merged evidence |
| --- | --- | --- |
| `StreemPilot/streempilot-api-server.rs` | Required Postgres; optional queue-only NATS; signaling client; explicit outbox-relay task; route/listener lifecycle. | PR #19, merge `bd6265e7e70f10d01458b7cb1deb7c79bd388c1c`; exact-head run `30907101712`. |
| `StreemPilot/streempilot-web-server.rs` | Axum routes/body limits, state, response security, bounded reference validation, handlers, and runtime. | PR #8, merge `e937f48e7c4732c998668fe04a0e85455e970f07`; exact-head run `30906047199`. |
| `StreemPilot/streempilot-mcp-server.rs` | API-origin allowlisting, bounded bearer HTTP, typed inputs, output ceiling, deterministic payloads, MCP routing, stdio lifecycle. | PR #4, merge `e3341a21d7f86dcfa526020b55eb8a8d60d64339`; exact-head run `30905898340`. |

All three services retain product-specific authorization, signaling, route, persistence, and domain policy. Rollback is by reviewed revert; shared history is not rewritten.

## Wave 2 media-router target

| Target | Starter responsibility | Repository state |
| --- | --- | --- |
| `StreemPilot/streempilot-media-router.rs` | Produce a deterministic bounded RTMP/SRT destination fan-out plan. | `provisioning_required` |

The starter explicitly does not implement the WebRTC signaling service, SFU, recording, compositing, provider credential storage, raw-media transport, API authority, or generic sync. Stream keys, provider tokens, raw media, SDP, ICE, and private media URLs remain outside route plans, logs, metrics, starter receipts, and issue/Linear evidence.

## Current PR and CI state — August 5, 2026

[StreemPilot/streempilot-monorepo#16](https://github.com/StreemPilot/streempilot-monorepo/pull/16) is the canonical current media-router starter PR. It semantically rebases the reviewed generator, tests, archive contract, and fleet documentation onto current `main`, superseding stale drafts #2 and #15.

Exact head:

```text
850a82afa51b3ee3f9581aa077bcc54aa489ff34
```

Current workflow state:

| Workflow | Run | State |
| --- | --- | --- |
| `fleet-contract` | `31033881293` | Queued for `[self-hosted, linux, sonus-ci]`. |
| `modular media-router starter` | `31033880887` | Queued for `[self-hosted, linux, sonus-ci]`. |

Queued is not passing evidence. PR #16 remains draft and must not merge until the exact head executes all contract, offline Cargo, rustfmt, strict Clippy, tests, startup-probe, deterministic archive, and media-boundary steps. Runner restoration is tracked in [StreemPilot/.github#1](https://github.com/StreemPilot/.github/issues/1).

## Repository provisioning sequence

After PR #16 is exact-head green and merged:

1. Verify or create `StreemPilot/streempilot-media-router.rs` with a reviewed repository-admin GitHub App.
2. Keep the repository private until release policy explicitly changes; enable issues/projects, disable wiki, and initialize `main`.
3. Download the exact reviewed starter artifact and verify both the GitHub artifact digest and internal checksum file.
4. Unpack into a repository-specific initialization branch.
5. Open a draft initialization PR.
6. Run offline locked Cargo metadata, rustfmt, strict Clippy, all-target tests, architecture tests, and startup probe.
7. Merge only the exact green reviewed head.
8. Add the exact child commit as a monorepo gitlink in a separate PR.
9. Update DEN-1757, this document, issues #1/#2, and the GitHub Project item with exact evidence.

A personal access token is not copied into GitHub or Linear. Repository creation must use a short-lived installation token from a least-privilege GitHub App, with exact target allowlisting, revocation, non-secret evidence, and temporary-key destruction.

## GitHub Project update contract

Add these durable items to [StreemPilot Project 1](https://github.com/orgs/StreemPilot/projects/1):

- `StreemPilot/.github#1` — hosted Actions/ARC capacity and required-check continuity.
- `StreemPilot/.github#2` — canonical release train and organization routing.
- `StreemPilot/streempilot-monorepo#16` — reviewed media-router starter.
- The media-router initialization PR after repository creation.

Suggested fields:

- Workstream
- Repository
- Linear ID
- Status
- Priority
- Release gate
- Blocked by
- Evidence

Projects v2 mutations require a Projects-capable App or authenticated GitHub CLI/GraphQL runner with project write permission. Until that exists, the issues and PR above are the stable board-ready inputs; no board mutation is claimed.

## Merge and evidence requirements

A PR is merge-ready only when:

- it is based on the current default branch;
- all conflicts are resolved semantically;
- the exact head has passed every required workflow;
- no unresolved review thread or changes-requested review remains;
- generated artifacts are content-addressed and reproducible;
- credentials, raw media, and private payloads are excluded from source, logs, reports, and artifacts; and
- Linear and organization documentation identify the exact head, workflow run, artifact digest, and merge commit.
