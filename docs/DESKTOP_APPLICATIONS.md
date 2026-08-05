# Desktop application allocation

Verified **2026-08-05**.

StreemPilot is allocated a paired native desktop streaming studio:

- Rust: [`StreemPilot/streempilot-desktop.rs`](https://github.com/StreemPilot/streempilot-desktop.rs) — **planned**, not yet verified as a published repository.
- Flutter: [`StreemPilot/streempilot-flutter-app`](https://github.com/StreemPilot/streempilot-flutter-app) — **planned**, not yet verified as a published repository.

The planned URLs are allocation targets, not proof that either remote exists. Do not mark an implementation live until the repository, native targets, media permissions, tests, packaging, signing, and supported-platform matrix are verified.

## Product boundary

Both implementations should support semantic parity for camera and microphone selection, permission handling, screen capture, scene and layout composition, guest/session control, local recording, streaming state, device persistence, audio/video diagnostics, background behavior, reconnect and recovery, and secure credential storage.

The Rust and Flutter implementations remain independently buildable, testable, releasable applications. Shared signaling/media contracts, schemas, clients, fixtures, sample scenes, device-state models, and conformance tests should be versioned deliberately.

## Feature-delivery rule

For every desktop-facing feature:

1. inspect both allocated repositories before deciding scope;
2. define shared acceptance criteria and identify affected contracts, devices, permissions, and fixtures;
3. create or update work for both implementations, or record an explicit no-change rationale;
4. test and report Rust and Flutter status separately for every supported operating system; and
5. keep reciprocal repository references, platform matrices, and recording/streaming safety assumptions current.

## Project routing

- GitHub Project: [`StreemPilot-project` — Project 1](https://github.com/orgs/StreemPilot/projects/1)
- Linear project: `github.com/streempilot`
- Central registry: [`ORESoftware/project-registry`](https://github.com/ORESoftware/project-registry/blob/main/registry/desktop-applications.json)
- Portfolio rollout: [`DEN-2469`](https://linear.app/denman/issue/DEN-2469/roll-out-paired-rust-flutter-desktop-repositories-across-the-portfolio)

Repository creation, renames, transfers, archival, or platform-status changes must update this document, the central registry, the Linear project, and both companion repositories in the same delivery.
