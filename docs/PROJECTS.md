<!-- org-project-routing:start -->
# Project routing

- **GitHub organization:** [StreemPilot](https://github.com/StreemPilot)
- **Canonical GitHub Project:** [StreemPilot-project](https://github.com/orgs/StreemPilot/projects/1) (project 1)
- **Canonical Linear project:** [planning workspace](https://linear.app/denman/project/githubcomstreempilot-e8b8f6dee124)
- **Organization documentation repository:** [StreemPilot/.github](https://github.com/StreemPilot/.github)

## Source-of-truth boundaries

GitHub is authoritative for repositories, commits, pull requests, reviews, CI checks, releases, deployable artifacts, and runtime evidence. Linear is authoritative for product planning, priorities, ownership, dependencies, milestones, and status reporting. The GitHub Project is the organization-level execution board and should contain the governance issue maintained by this repository.

## Change and merge policy

Documentation branches must be reviewed through pull requests and merged after checks pass. Concurrent edits are reconciled semantically against the latest default branch: this managed routing block is regenerated while all unrelated prose outside the block is preserved. Do not resolve conflicts by blindly choosing one side.
<!-- org-project-routing:end -->

## Rust server modularization program

The cross-organization Rust-server program is tracked in Linear by [DEN-1682](https://linear.app/denman/issue/DEN-1682), [DEN-1757](https://linear.app/denman/issue/DEN-1757), and repository-publication reconciliation [DEN-2328](https://linear.app/denman/issue/DEN-2328). The organization-specific technical and operational ledger is [RUST_SERVER_MODULARIZATION.md](./RUST_SERVER_MODULARIZATION.md).

### Current StreemPilot state

| Unit | GitHub evidence | State |
| --- | --- | --- |
| API runtime | `StreemPilot/streempilot-api-server.rs#19` | Merged; Postgres/NATS/signaling bootstrap and outbox-task ownership are modularized. |
| Web runtime | `StreemPilot/streempilot-web-server.rs#8` | Merged; routes, state, validation, security middleware, Playwright, and runtime lifecycle are modularized. |
| MCP runtime | `StreemPilot/streempilot-mcp-server.rs#4` | Merged; configuration, bounded bearer HTTP, typed models, rendering, tools, and stdio lifecycle are modularized. |
| Media router | [`StreemPilot/streempilot-media-router.rs`](https://github.com/StreemPilot/streempilot-media-router.rs), repository `1324470250`, `main` `a3b01146f85ee61400b72ed3f333c76b4413a4fa` | Published private; exact reviewed sealed history verified. |

The media-router source is sealed in the reviewed 32-repository fleet at `ORESoftware/ai-agent-coordinator.rs@5d9a0c2cb44dff607bc3953954ce4b9af08e5789`. Trusted-main run `31045540736` preserved the three exact HypeSiege repositories, created the canonical StreemPilot repository, and verified the combined result as 4/4. Bounded evidence is merged in `ORESoftware/k8s-cluster#1069` at `4e9df62da54479c9f52d850c16703b5e112bb282`. Artifact `8946360080` has SHA-256 `c87ff38d687d81def5c419297dc28445d6cf659ef1d262c3c02d6b4a18ed99ec`.

The immutable fleet ledger records the owner in lowercase, while GitHub returns the canonical organization spelling `StreemPilot`. Publication and evidence compare owner/repository identity case-insensitively, reject duplicate identities, retain the exact one-repository mutation boundary, and emit GitHub's canonical `StreemPilot/streempilot-media-router.rs` identity.

### GitHub Project fields

Use these organization-wide fields for the release train and Rust program:

- **Workstream:** Foundation, Contracts, API, Studio, Media, Destinations, Recording, Sync, Automation, E2E, Infrastructure.
- **Repository:** exact `owner/name` identity.
- **Linear ID:** DEN issue identifier.
- **Status:** Backlog, Ready, In progress, In review, Blocked, Done.
- **Priority:** Urgent, High, Normal, Low.
- **Release gate:** exact PR, check, artifact, or environment gate.
- **Blocked by:** issue, credential class, capacity lane, or repository prerequisite.
- **Evidence:** exact head SHA, workflow run, artifact digest, and merge commit.

Keep `StreemPilot/.github#1`, `StreemPilot/.github#2`, the media-router repository follow-up PR, DEN-2328, and the merged evidence PR linked to [StreemPilot Project 1](https://github.com/orgs/StreemPilot/projects/1). The current connector does not expose Projects v2 item mutation, so the durable issues and this ledger remain the board-ready source until a Projects-capable GitHub App or authenticated `gh project` runner performs the item updates.

### Credential and media boundary

Do not place personal access tokens, runner-registration tokens, GitHub App private keys, stream keys, provider access/refresh tokens, raw media, SDP, ICE, or private media URLs in commits, workflow inputs, issue bodies, PR descriptions, artifacts, logs, or Linear. The August 5 publication used a one-time run-bound RSA-OAEP handoff after the protected host proved that no repository-admin App key material was available. Exactly one ciphertext was accepted, the decrypted credential was masked and held only in a mode-0600 runner-temporary file, and all credential material was destroyed unconditionally. Permanent repository administration should use reviewed least-privilege GitHub Apps with short-lived installation tokens and non-secret evidence. Any PAT pasted into chat must be revoked or rotated.
