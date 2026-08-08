# StreemPilot organization defaults

This public `.github` repository contains organization-wide community health files, contributor guidance, shared agent policy, repository boundaries, the StreamYard-parity roadmap, and GitHub/Linear project synchronization guidance.

Repository-local policy wins when it is stricter or more specific. Existing project history must be preserved during consolidation and conflict resolution.

## Organization planning

- [Canonical repository boundaries](REPOSITORY_BOUNDARIES.md)
- [StreamYard-parity roadmap](STREAMYARD_PARITY_ROADMAP.md)
- [GitHub and Linear project synchronization](PROJECT_SYNC.md)
- [Branching and deployment](BRANCHING_AND_DEPLOYMENT.md)
- [Organization release train issue](https://github.com/StreemPilot/.github/issues/2)
- [Actions and ARC capacity issue](https://github.com/StreemPilot/.github/issues/1)

The active mirrored Linear project is `github.com/streempilot`. GitHub owns exact code/review/check evidence; Linear owns cross-repository planning, dependencies, milestones, and project documentation.

<!-- ore-org-baseline:begin -->
## Account-wide defaults

This public repository is the canonical source for GitHub-supported fallback community files, organization profile content, reusable workflow examples, and public contributor guidance for [`StreemPilot`](https://github.com/StreemPilot).

- GitHub owner: [`StreemPilot`](https://github.com/StreemPilot)
- Linear project: [github.com/streempilot](https://linear.app/denman/project/githubcomstreempilot-e8b8f6dee124)
- Public context: [`ORG_CONTEXT.md`](ORG_CONTEXT.md)
- Canonical agent policy for this repository: [`agents.md`](agents.md)
- Governance: [`GOVERNANCE.md`](GOVERNANCE.md)
- Public repository graph: [`repository-relationships.json`](repository-relationships.json)
- Relationship guide: [`docs/REPOSITORY_RELATIONSHIPS.md`](docs/REPOSITORY_RELATIONSHIPS.md)
- Security reporting: [`SECURITY.md`](SECURITY.md)

GitHub applies only its documented fallback community files automatically. Agent instructions, relationship files, and reusable workflows are **not copied into sibling repositories**; repositories that need local enforcement must carry their own lowercase `agents.md` and explicitly call or copy the provided workflow.

`repository-relationships.json` is generated from GitHub owner membership plus reviewed declarations in `repository-relationships.manual.json`. It is public-safe: private repository names are omitted. The complete graph is synchronized separately to the approved private project registry.

## Safety baseline

Changes are pull-request driven. Contributors and agents must preserve concurrent work, avoid destructive Git operations, resolve conflicts semantically with full history and cross-repository context, validate affected contracts, and never claim a remote action completed without authoritative evidence.

Generated baseline version: `2026-08-04`.
<!-- ore-org-baseline:end -->
