# StreemPilot repository boundaries

Every repository has one primary responsibility and an explicit dependency direction. Repository-local policy wins when it is stricter.

## Canonical short-name family

| Repository | Primary responsibility | May depend on | Must not own |
| --- | --- | --- | --- |
| `sp-interfaces` | Durable schemas, OpenAPI/AsyncAPI, NATS subjects, WebRTC control contracts, cross-language fixtures | none of the deployable services | product runtime policy, credentials, deployment |
| `sp-api` | Small Rust/Axum REST and WebSocket bootstrap/control facade | `sp-interfaces`, eventually `sp-libs` | media relay, provider credentials, duplicated durable schema |
| `sp-web-mash` | Production MASH studio: Maud, Axum, SeaORM, Supabase integration, HTMX, browser WebRTC controls | `sp-interfaces`, `sp-libs`, `sp-sync`, API clients | SFU/media routing, TURN secrets, provider egress |
| `sp-web-leptos` | Independently deployable Leptos SSR studio surface | shared contracts and reviewed API/control clients | unauthenticated public realtime broadcast, raw media relay |
| `sp-web-dioxus` | Independently deployable Dioxus SSR studio surface and future desktop-friendly shell | shared contracts and reviewed API/control clients | unauthenticated public realtime broadcast, raw media relay |
| `sp-cli` | Operator automation using `flags-2-env`, clients, interfaces, and reusable libraries | `sp-clients`, `sp-interfaces`, `sp-libs` when published | raw stream keys on argv, server-only policy |
| `sp-sync` | Product-specific offline reconciliation over immutable Opto Sync primitives | `opto-sync/syncer.rs`, `sp-interfaces` where needed | live presence, SDP/ICE, media, provider credentials |
| `sp-infra` | StreemPilot-specific deployment declarations and environment overlays | published images and contract versions | application business logic or reusable source packages |

## Canonical supporting repositories

| Repository | Responsibility |
| --- | --- |
| `streempilot-clients` | Current SDK source and transport adapters; migrate deliberately to the short `sp-clients` identity without losing history or consumers. |
| `streempilot-e2e` | Black-box browser, API, signaling, sync, network, accessibility, and release verification. |
| `streempilot-monorepo` | Workspace, migration, provisioning, and release ledger; it is not the canonical deployable source when a standalone repository exists. |
| `.github` | Organization policy, roadmap, project synchronization, community files, and repository-family governance. |

## Mature long-name API train

`streempilot-api-server.rs` contains mature SeaORM/RDS, Supabase/shared-auth, signaling admission, TURN, scene, comment, destination, recording, and outbox work that is not yet semantically consolidated into `sp-api`.

Do not archive, overwrite, or mechanically choose one API repository. Consolidation requires a route-by-route, migration-by-migration, event-by-event, test-by-test conceptual merge. Preserve unique production behavior and stable consumers.

## Missing package boundary

`sp-libs` is planned but not yet provisioned or published. It will own reusable runtime-light domain validation, serialization, studio-state, and signaling-adapter logic and depend on `sp-interfaces`.

Until the package resolves immutably:

- do not fabricate `.zpkg.lock`;
- do not leave active manifests pointing to the nonexistent coordinate;
- track provisioning in `streempilot-monorepo#10` and `streempilot-clients#6`;
- keep product/server-only concerns out of the future library.

## Realtime and media boundary

Generic REST/WebSocket control services may carry bounded identity, presence, subscription, scene, overlay, destination intent, revision, health, and receipt metadata. They must not carry raw audio/video, encoded media, SDP, ICE credentials/candidates, stream keys, raw RTMP URLs, OAuth/access/refresh tokens, signed media URLs, or provider credentials.

WebRTC signaling, TURN, SFU/media routing, compositing, recording bytes, and destination egress are separate bounded services.

## Package and composition rules

- `sp-libs -> sp-interfaces`
- `sp-clients -> sp-interfaces + sp-libs`
- `sp-cli -> sp-clients + sp-interfaces + sp-libs`
- API/web/backend -> `sp-interfaces + sp-libs + sp-sync` as applicable
- MCP -> clients, interfaces, libraries, CLI, sync, and shared-auth clients
- E2E -> clients, interfaces, libraries, and CLI

Zed owns reusable package resolution. A retained gitlink must be classified as `workspace`, `inventory`, `embedded-source`, `experiment-reference`, or `legacy`. Never represent the same dependency through both Zed and a git submodule in one composition.

## Consolidation policy

When repositories overlap:

1. identify the canonical responsibility;
2. compare complete commit history, routes, contracts, migrations, tests, workflows, deployment files, and consumers;
3. perform a semantic merge that preserves the best behavior from both sides;
4. migrate callers and release coordinates;
5. preserve attribution and useful history;
6. leave a clear deprecation or redirect pointer;
7. archive only after production and rollback evidence exists.
