# StreemPilot Rust server modularization and provisioning ledger

This document is the StreemPilot organization view of the cross-organization program tracked by Linear [DEN-1682](https://linear.app/denman/issue/DEN-1682), [DEN-1757](https://linear.app/denman/issue/DEN-1757), and repository-publication reconciliation [DEN-2328](https://linear.app/denman/issue/DEN-2328).

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

## Wave 2 media-router publication

| Repository | Responsibility | Verified publication state |
| --- | --- | --- |
| [`StreemPilot/streempilot-media-router.rs`](https://github.com/StreemPilot/streempilot-media-router.rs) | Produce a deterministic bounded RTMP/SRT destination fan-out plan. | Private repository `1324470250`; `main` `a3b01146f85ee61400b72ed3f333c76b4413a4fa`; exact sealed history verified. |

The starter explicitly does not implement the WebRTC signaling service, SFU, recording, compositing, provider credential storage, raw-media transport, API authority, or generic sync. Stream keys, provider tokens, raw media, SDP, ICE, and private media URLs remain outside route plans, logs, metrics, starter receipts, and issue/Linear evidence.

## Repository publication result — August 5, 2026

Trusted-main GitHub Actions run `31045540736` authenticated as `ORESoftware`, reconstructed the exact 32-repository source fleet—888 tracked files and 30 gitlinks—and verified the combined HypeSiege/StreemPilot publication as 4/4. It preserved three exact HypeSiege repositories and created the StreemPilot media router privately on `main` at reviewed sealed SHA `a3b01146f85ee61400b72ed3f333c76b4413a4fa`.

Bounded non-secret evidence is merged in [ORESoftware/k8s-cluster#1069](https://github.com/ORESoftware/k8s-cluster/pull/1069) as commit `4e9df62da54479c9f52d850c16703b5e112bb282`. Artifact `8946360080`, `den-2328-encrypted-exact-gaps-31045540736`, has SHA-256 `c87ff38d687d81def5c419297dc28445d6cf659ef1d262c3c02d6b4a18ed99ec`.

The final exact result is:

```text
created=1 preserved_exact=3 verified=4 failures=0
```

The immutable fleet ledger records `streempilot/streempilot-media-router.rs`; GitHub returns the canonical organization spelling `StreemPilot`. The reviewed publication repair compares identities case-insensitively, rejects case-insensitive duplicates and cross-owner escapes, invokes the sealed publisher with its immutable source identity, and records GitHub's canonical owner spelling in evidence.

## Repository-local follow-up sequence

1. Open a focused follow-up branch and PR; do not rewrite the sealed bootstrap commit.
2. Add canonical Project/Linear routing and repository-specific media-router operational ownership.
3. Run offline locked Cargo metadata, rustfmt, strict Clippy, all-target tests, architecture tests, and startup probes already defined by the starter.
4. Preserve the signaling/media/recording/compositing/provider credential boundaries with tests.
5. Merge only the exact green reviewed head.
6. Add or update the exact child commit as a monorepo gitlink in a separate PR.
7. Update DEN-1757, DEN-2328, this document, issues #1/#2, and the GitHub Project item with exact evidence.

The separately audited historical identity `StreemPilot/streempilot-flutter-app`, which currently redirects to `StreemPilot/sp-web-leptos`, is not part of this four-repository publication and remains a distinct redirect-restoration decision. It must not be silently added to this evidence set.

## GitHub Project update contract

Keep these durable inputs linked to [StreemPilot Project 1](https://github.com/orgs/StreemPilot/projects/1):

- `StreemPilot/.github#1` — hosted Actions/ARC capacity and required-check continuity;
- `StreemPilot/.github#2` — canonical release train and organization routing;
- the media-router follow-up PR;
- DEN-2328 and the merged evidence PR.

Use fields `Workstream`, `Repository`, `Linear ID`, `Status`, `Priority`, `Release gate`, `Blocked by`, and `Evidence`. The current connector does not expose Projects v2 item mutation; the issues, PRs, and this ledger are the stable board-ready inputs for a Projects-capable GitHub App or authenticated `gh project` runner.

## Credential and media boundary

The protected GitHub App path failed before mutation because no repository-admin App ID/private-key pair was present. The successful publication therefore used an exceptional one-time RSA-OAEP handoff bound to one Actions run and issue. Exactly one ciphertext was accepted; the decrypted PAT was immediately masked, held only in a mode-0600 runner-temporary file, and destroyed with the keypair and payload in unconditional cleanup. No plaintext credential, stream key, provider token, raw media, SDP, ICE, or private media URL entered source, workflow configuration, artifacts, issue text, PR text, logs, or Linear. Permanent organization administration should use reviewed least-privilege GitHub App installation tokens. Any PAT pasted into chat must be revoked or rotated.

## Merge and evidence requirements

A PR is merge-ready only when:

- it is based on the current default branch;
- all conflicts are resolved semantically;
- the exact head has passed every required workflow;
- no unresolved review thread or changes-requested review remains;
- generated artifacts are content-addressed and reproducible;
- credentials, raw media, and private payloads are excluded from source, logs, reports, and artifacts; and
- Linear and organization documentation identify the exact head, workflow run, artifact digest, and merge commit.
