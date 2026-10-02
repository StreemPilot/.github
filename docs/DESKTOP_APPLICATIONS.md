# Desktop application allocation

Verified **2026-08-06**.

StreemPilot is allocated a paired desktop streaming studio:

- Rust: [`StreemPilot/streempilot-desktop.rs`](https://github.com/StreemPilot/streempilot-desktop.rs) — **planned**, not yet verified as a published repository.
- Flutter canonical target: `StreemPilot/streempilot-flutter` — **planned**, not yet verified as a published repository.

Earlier planning used `streempilot-flutter-app`; the shorter `streempilot-flutter` name is canonical unless an explicit ADR changes it. Neither planned URL is proof that a remote exists.

## Why both Rust and Flutter remain active

The two studio applications will be first-class side-by-side implementations so the product can compare capture reliability, latency, CPU/GPU use, device integration, accessibility, Flutter mobile reuse, developer velocity, packaging/signing, and long-term maintenance with the same streaming features.

Every desktop-facing feature must be planned against both repositories, share acceptance criteria and simulated media/device fixtures, and normally update both. A one-sided change requires a documented no-change rationale and parity gap.

## Rust desktop kit: Rust + Qt through FFI

**Selected strategy:** Rust domain/media-control logic with Qt presentation and multimedia integration through a narrow typed FFI boundary, preferably CXX-Qt or an equivalently reviewed bridge.

**WebView policy:** prohibited for the Rust studio.

StreemPilot requires mature camera, microphone, screen-capture, GPU, scene composition, multi-window, local-recording, and audio/video diagnostic capabilities. Qt provides native multimedia/windowing facilities while Rust owns signaling, session state, permissions policy, recording orchestration, persistence, concurrency, and security-sensitive logic.

FFI rules:

- expose narrow typed commands and value models;
- keep credentials, signaling, session state, recording policy, and persistence in Rust;
- let Qt own presentation, native devices, capture surfaces, window events, and accessibility;
- avoid broad QObject exposure and untyped QVariant maps at security boundaries; and
- test ABI ownership, thread handoff, device loss, cancellation, and recovery.

The Rust repository must contain `docs/DESKTOP_TOOLKIT.md` covering Qt/FFI version policy, capture/media boundary, permissions, deep links, tests, packaging/signing, and Flutter companion.

## HTTPS-first deep linking

Canonical form:

```text
https://<verified-streempilot-owned-host>/open/<route>?<bounded-query>
```

Fallback scheme:

```text
streempilot://<route>?<bounded-query>
```

Routes must be defined in `sp-interfaces` and shared by Rust, Flutter, clients, signaling services, and browser fallback pages.

Required behavior:

- support cold start and already-running delivery;
- validate the exact host, route, studio/session/scene/guest identifiers, action, and bounded query parameters before crossing FFI;
- never place streaming credentials, private recordings, room secrets, signaling tokens, media payloads, or personal data in URLs;
- use short-lived, one-time, audience-bound codes for guest invitations, authentication, and session joins;
- require explicit confirmation before joining a live session, enabling capture, or starting a recording;
- preserve a pending route safely through authentication and device permission prompts; and
- test macOS, Windows, Linux, Android, and iOS app/universal links plus browser fallback.

Qt receives OS URL/file-open events, but the shared Rust parser validates and authorizes routes before any device, signaling, or recording action.

## Product boundary

Both implementations should support semantic parity for camera/microphone selection, permissions, screen capture, scene/layout composition, guest/session control, local recording, streaming state, device persistence, diagnostics, background behavior, reconnect/recovery, secure credential storage, and deep links.

Shared signaling/media contracts, schemas, clients, route fixtures, simulated devices, sample scenes, device-state models, and conformance tests must be versioned deliberately.

## Repository creation requirements

Both repositories must begin as buildable scaffolds, not placeholders. The Rust repo must include `docs/DESKTOP_TOOLKIT.md`, reciprocal README/AGENTS/PR guidance, native CI/package/signing skeletons, simulated capture smoke tests, permission tests, and shared contract fixtures.

Central toolkit assignments: [`rust-desktop-strategies.md`](private-registry://canonical/registry/rust-desktop-strategies.md).

## Project routing

- GitHub Project: [`StreemPilot-project` — Project 1](https://github.com/orgs/StreemPilot/projects/1)
- Linear project: `github.com/streempilot`
- Central registry: [`approved-private-registry`](private-registry://canonical/registry/desktop-applications.json)
- Portfolio rollout: [`DEN-2469`](https://linear.app/denman/issue/DEN-2469/roll-out-paired-rust-flutter-desktop-repositories-across-the-portfolio)

Repository creation, naming changes, toolkit/FFI changes, deep-link changes, transfers, archival, or platform-status changes must update this document, the central registry/strategy, Linear, and both companion repositories in the same delivery.
