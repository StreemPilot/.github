# StreemPilot organization handbook

> Shared operating defaults for repositories maintained under **StreemPilot**. Repository-local policy may strengthen these rules but should not silently weaken them.

## Mission

StreemPilot maintains live-stream production, orchestration, browser, media-routing, and operational control software. This `.github` repository is the canonical home for shared policy, reusable templates, community health files, and planning links.

## Repository contract

Each active repository must document purpose, ownership, maturity, supported browsers and platforms, development and test commands, authoritative signaling and media interfaces, release and rollback procedures, compatibility policy, and GitHub Project/Linear links. Streaming components should also document session lifecycle, codec and device assumptions, signaling, permissions, reconnection, latency, backpressure, recording, provider limits, observability, and degraded modes.

## Change workflow

1. Anchor work in an issue, Linear item, or documented maintenance objective.
2. Keep branches and pull requests focused.
3. Explain motivation, scope, live-session and compatibility risk, validation, migration, and rollback.
4. Test permission denial, device changes, reconnect, packet loss, timeout, overload, partial failure, and browser/version variation as relevant.
5. Resolve conflicts semantically by reconstructing both sides' intent.
6. Prefer squash merges for focused work unless commit structure materially improves auditability.

## Evidence, security, and documentation

Pull requests should include reproducible commands, synthetic media fixtures, expected and observed behavior, browser/device coverage, negative-path evidence, documentation updates, and CI or local-equivalent results. Never commit credentials, private streams, signing material, provider tokens, or sensitive logs. Follow `SECURITY.md` for private reporting. Keep media and signaling boundaries explicit, examples sanitized, compatibility matrices current, and important privacy, reliability, and operational decisions recorded.

## Planning ownership

GitHub owns code, reviews, checks, releases, and delivery evidence. Linear owns priority, dependencies, sequencing, and cross-project planning. The organization GitHub Project is the cross-repository execution view; see `PROJECTS.md` for routing details.

## Organization health

- [ ] Profiles, descriptions, topics, and READMEs are current.
- [ ] Community health files and reusable issue/PR guidance are present.
- [ ] Session, signaling, media, permissions, reconnect, latency, recording, and degraded behavior are documented.
- [ ] Required checks cover representative browsers/devices, network failure, compatibility, privacy, and supply-chain risk.
- [ ] Stale repositories are archived or clearly marked.
- [ ] GitHub Project and Linear links resolve and reflect completed work.
