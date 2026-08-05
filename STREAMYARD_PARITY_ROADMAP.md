# StreemPilot StreamYard-parity roadmap

Last updated: 2026-08-05

This roadmap defines parity as production capability with security, reliability, accessibility, operability, and recovery evidence—not visual resemblance or a checklist of mock controls.

Organization tracking:

- release train: [StreemPilot/.github#2](https://github.com/StreemPilot/.github/issues/2)
- Actions/ARC capacity gate: [StreemPilot/.github#1](https://github.com/StreemPilot/.github/issues/1)
- Linear project: `github.com/streempilot`

## Foundations already established

- canonical `sp-*` repositories exist for interfaces, API, MASH, Leptos, Dioxus, CLI, sync, and infrastructure;
- `sp-api#3` repaired the bootstrap transport ownership boundary;
- `sp-web-leptos#7` and `sp-web-dioxus#7` replaced unsafe realtime prototypes with loopback-default, same-origin, bounded control sockets;
- `sp-cli#6` removed an unresolved package coordinate from the active `dev` graph;
- `sp-sync#4` established the canonical Rust Opto Sync adapter under `rust/`;
- the mature long-name API and MASH histories remain available for semantic consolidation rather than destructive replacement.

## Capability matrix

| Capability | Canonical owner | Release evidence |
| --- | --- | --- |
| Accounts, workspaces, roles, device trust | `sp-api`, mature API, shared-auth | cross-tenant 404/403 isolation, token expiry, role matrix, audit events |
| Scheduled and reusable broadcasts | API + MASH/clients | create/edit/replay/idempotency, timezone handling, recovery after restart |
| Guest lobby and backstage | API + signaling + studio surfaces | invitation expiry, admit/remove, reconnect, role transitions, abusive-client limits |
| Camera, microphone, screen share | browser/native capture + signaling/media plane | permission denial, device switching, mute state, screen-share lifecycle, reconnect |
| Scenes, layouts, branding, overlays | `sp-web-mash`, API contracts | preview/program separation, revision conflicts, accessibility, responsive layouts |
| Audience comments and private chat | API/chat service + MASH | official provider adapters, moderation, escaping, one-featured invariant, retries |
| Multistream destinations | API, destination workers, media router | reusable outputs, RTMP/SRT/WebRTC adapters, retries, receipts, aggregate health |
| Recording and isolated tracks | recording service + MASH recovery | local/cloud recovery, checksums, resumable upload, isolated/composite validation |
| Clips, captions, webinars | dedicated workers and studio UI | bounded jobs, provider failures, accessibility, downloadable evidence |
| Offline project editing | `sp-sync` + clients | restart persistence, idempotent replay, visible conflicts, tombstones, secret exclusion |
| CLI and agent automation | `sp-cli`, future MCP server | `flags-2-env`, scoped credentials, dry-run/revision gates, stable JSON, audit history |
| Analytics and operations | analytics/observability services | broadcast quality, destination health, audience metrics, SLOs, incident evidence |

## Architecture invariants

1. PostgreSQL and revisioned API commands remain authoritative for durable state.
2. WebSockets carry bounded control metadata, not raw media or provider secrets.
3. WebRTC signaling is distinct from TURN, SFU/media routing, composition, recording, and destination egress.
4. Stream keys, raw RTMP URLs, OAuth/access/refresh tokens, signed media URLs, SDP, and ICE credentials never enter generic logs, issues, Linear, offline sync, or MCP payloads.
5. Public or alternate studio surfaces default to loopback or require an explicit reviewed exposure path.
6. Every externally reachable socket has origin/authentication policy, byte limits, command/topic allowlists, rate limits, heartbeat behavior, and backpressure/lag semantics.
7. Required checks are not bypassed because one runner lane is unavailable.

## Release sequence

### 1. Repository and package graph

- create and publish `sp-libs`;
- converge `streempilot-clients` to `sp-clients` without losing history;
- resolve Zed packages immutably and generate lockfiles through the resolver;
- compare and semantically consolidate `sp-api` with `streempilot-api-server.rs`;
- classify monorepo submodules and remove duplicate dependency representations.

### 2. Studio control plane

- complete the MASH studio train and reduce `sp-web-mash#12` to the canonical production scope now that standalone Leptos/Dioxus hardening has landed;
- align all three studio surfaces on contract fixtures, origin/auth policy, error codes, heartbeats, and topic schemas;
- wire the authenticated API WebSocket/client SDK surface without creating a second WebRTC signaling implementation.

### 3. Media plane

- provision the reviewed media-router repository from `streempilot-monorepo#16`;
- implement TURN/SFU topology, simulcast/SVC strategy, active-speaker state, bandwidth adaptation, and region selection;
- implement compositor, isolated-track and composite recording, destination fan-out, retry/receipt workflows, and bounded provider adapters.

### 4. Reliability and security

- restore Actions capacity and certify AWS/Hetzner ARC fallback;
- add network-loss, packet-loss, latency, reconnect, browser-crash, worker-crash, and provider-outage tests;
- prove tenant isolation, credential exclusion, replay/idempotency, revision conflict, tombstone, and rollback behavior;
- enforce SBOM, provenance, immutable images, secret scanning, dependency audits, and deployment policy.

### 5. Product release

- accessibility and keyboard/screen-reader validation;
- narrow/mobile, desktop, and multi-window producer workflows;
- user documentation, operational runbooks, support and incident playbooks;
- staging rehearsal, canary, rollback, and production evidence;
- final parity report linked to DEN-918.

## Definition of done

Parity is reached only when representative host, producer, guest, viewer, and automation journeys run against real services and durable data with:

- no mocks in release evidence;
- successful recovery from expected failures;
- secret-free logs and artifacts;
- exact versioned contracts and dependency provenance;
- measured media quality and destination health;
- accessibility evidence;
- a proven rollback path.
