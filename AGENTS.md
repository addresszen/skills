# Agent Skills (AddressZen)

Distribution repo for AddressZen skills. Skills are authored in a private upstream monorepo and mirrored here.

## Source of Truth

The private upstream monorepo is the canonical source:

- **Path:** `packages/skills-zen/`
- **Authoring:** see `CLAUDE.md` in that directory
- **Version:** managed via Changesets alongside other packages

## This Repo

This public mirror at `addresszen/skills`:

- Tracks the latest release of all skills from upstream
- Is distribution-only (tagged releases for agent tooling to discover)
- Accepts issues and PRs from the community

## Contributing

To contribute changes:

1. **File an issue** here describing the problem or suggestion
2. **Propose a PR** with changes to skill files
3. A maintainer will review, cherry-pick the changes upstream, and merge them back here on the next release

## License

See LICENSE in LICENSE
