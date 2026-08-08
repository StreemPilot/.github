# StreemPilot marketing site

Complete Astro source staged for the future public repository `StreemPilot/StreemPilot.github.io` and URL `https://streempilot.github.io/`.

## Canonical planning

- Linear project: `github.com/StreemPilot`
- GitHub Project: [StreemPilot project #1](https://github.com/orgs/StreemPilot/projects/1)
- Official client source: [streempilot-clients](https://github.com/StreemPilot/streempilot-clients)
- Organization: [StreemPilot](https://github.com/StreemPilot)

## Client truth

`streempilot-clients` defines a canonical OpenAPI contract plus TypeScript, Dart, and Rust clients for broadcast management, signaling sessions and ICE exchange, and multistream preflight orchestration. The repository currently describes its server-facing TypeScript surface as simulated until the live APIs are implemented. The page says that explicitly: the clients and schemas are real, while end-to-end service availability is not represented as complete.

## Publish

1. Create public repository `StreemPilot.github.io` in the `StreemPilot` organization.
2. Copy this directory to the new repository root.
3. Run `npm install && npm run build`.
4. Add the standard Astro GitHub Pages workflow and enable GitHub Actions as the Pages source.
5. Verify `https://streempilot.github.io/` and update the linked GitHub and Linear tickets.
