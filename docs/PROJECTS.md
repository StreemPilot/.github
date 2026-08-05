<!-- org-project-routing:start -->
# Project routing

- **GitHub organization:** [StreemPilot](https://github.com/StreemPilot)
- **Canonical GitHub Project:** [StreemPilot-project](https://github.com/orgs/StreemPilot/projects/1) (project 1)
- **Canonical Linear project:** [github.com/StreemPilot](https://linear.app/denman/project/githubcomstreempilot-e8b8f6dee124)
- **Organization documentation repository:** [StreemPilot/.github](https://github.com/StreemPilot/.github)
- **Durable organization routing card:** [StreemPilot/.github#2](https://github.com/StreemPilot/.github/issues/2)
- **CI-capacity restoration card:** [StreemPilot/.github#1](https://github.com/StreemPilot/.github/issues/1)

## Source-of-truth boundaries

GitHub is authoritative for repositories, commits, pull requests, reviews, CI checks, releases, deployable artifacts, and runtime evidence. Linear is authoritative for product planning, priorities, ownership, dependencies, milestones, and status reporting. The GitHub Project is the organization-level execution board and should contain the governance issue maintained by this repository.

## Change and merge policy

Documentation branches must be reviewed through pull requests and merged after checks pass. Concurrent edits are reconciled semantically against the latest default branch: this managed routing block is regenerated while all unrelated prose outside the block is preserved. Do not resolve conflicts by blindly choosing one side.
<!-- org-project-routing:end -->

## Rust server modularization program

The cross-organization Rust-server program is tracked in Linear by [DEN-1682](https://linear.app/denman/issue/DEN-1682) and [DEN-1757](https://linear.app/denman/issue/DEN-1757). The organization-specific technical and operational ledger is [RUST_SERVER_MODULARIZATION.md](./RUST_SERVER_MODULARIZATION.md).

### Current StreemPilot state

| Unit | GitHub evidence | State |
| --- | --- | --- |
| API runtime | `StreemPilot/streempilot-api-server.rs#19` | Merged; Postgres/NATS/signaling bootstrap and outbox-task ownership are modularized. |
| Web runtime | `StreemPilot/streempilot-web-server.rs#8` | Merged; routes, state, validation, security middleware, Playwright, and runtime lifecycle are modularized. |
| MCP runtime | `StreemPilot/streempilot-mcp-server.rs#4` | Merged; configuration, bounded bearer HTTP, typed models, rendering, tools, and stdio lifecycle are modularized. |
| Media-router starter | `StreemPilot/streempilot-monorepo#16` | Open draft; exact head is waiting for self-hosted `sonus-ci` runner assignment. Target repository remains unprovisioned. |

PR #16 semantically rebases the reviewed media-router starter onto the current fleet ledger. Its exact-head `fleet-contract` and `modular media-router starter` runs are queued on `[self-hosted, linux, sonus-ci]`; neither may be treated as passing until a runner executes every step. GitHub-hosted Actions and the AWS/Hetzner ARC path are tracked by issue #1.

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

Projects v2 write access is now available through the reviewed, rate-aware GitHub CLI/GraphQL reconciler. Keep issues #1 and #2 plus linked implementation issues current as stable board inputs. A Project mutation is claimed only when the fleet evidence records and live-verifies the exact organization, Project, and item; chat history is never the evidence source.

### Credential and media boundary

Do not place personal access tokens, runner-registration tokens, GitHub App private keys, stream keys, provider access/refresh tokens, raw media, SDP, ICE, or private media URLs in commits, workflow inputs, issue bodies, PR descriptions, artifacts, logs, or Linear. Repository and runner administration must use reviewed least-privilege GitHub Apps with short-lived installation tokens and non-secret evidence.
