<p align="center">
  <a href="https://docleus.io"><img src="./.github/assets/docleus.svg" width="88" alt="Docleus logo" /></a>
</p>

<h1 align="center">Docleus Community</h1>

<p align="center">
  <strong>A shared home for contributors.</strong><br />
  Community guidance, organization profile, and source-aware CI for Docleus.
</p>

<p align="center">
  <a href="LICENSE"><img alt="MIT license" src="https://img.shields.io/badge/license-MIT-111111?style=flat-square" /></a>
  <img alt="Public preview in preparation" src="https://img.shields.io/badge/preview-0.0.1-cfcfcf?style=flat-square" />
  <a href="https://docleus.io"><img alt="Online documentation" src="https://img.shields.io/badge/docs-docleus.io-111111?style=flat-square" /></a>
</p>

<p align="center">
  <a href="https://docleus.io">Documentation</a> &middot;
  <a href="#reusable-ci">Reusable CI</a> &middot;
  <a href="https://github.com/Docleus/docleus">Run Docleus</a> &middot;
  <a href="https://github.com/Docleus/.github/blob/main/CONTRIBUTING.md">Contribute</a>
</p>

---

Published as `Docleus/.github`: the organization profile, contribution and
security guidance, issue/PR templates, and the reusable CI workflow.

## Reusable CI

`.github/workflows/ci.yml` checks out core, the official plugins, and the
source distribution side by side. It installs with frozen lockfiles, builds
core and the plugins, and runs the caller's `pnpm check`. Repositories with
browser tests also run Chromium acceptance tests. This layout is required by
the packages' local `link:` dependencies; checking out a plugin alone is not
sufficient.

```yaml
permissions:
  contents: read

jobs:
  check:
    uses: Docleus/.github/.github/workflows/ci.yml@main
    with:
      repository-name: docleus-plugin-editor
      run-e2e: true
```

The caller's exact revision is retained. `core-ref` and `siblings-ref` default
to `main`; maintainers can select reviewed commits or release tags when
validating another compatibility target. Release tags are not assumed to exist
before the first release. All sibling repositories must be available publicly
for the read-only checkout flow; private repositories need a separately
approved authentication setup. Publish this workflow before enabling callers.

Core and plugin checks include typecheck, lint, formatting, dependency
boundaries, licenses, and unit/in-process integration tests. The distribution's
`pnpm check` runs its Node integration tests. Docker, Postgres, real S3, and Dex
acceptance are separate release gates, not implied by a green CI job.

No workflow commits, tags, pushes, publishes packages, or uploads images.
Review and pin the reusable workflow and action refs to approved immutable
commits before the final release freeze. The first hosted run is still required
before treating CI as verified.

## Community files

- `profile/README.md`: organization profile.
- `CONTRIBUTING.md`: source setup and contribution checks.
- `SECURITY.md`: pre-1.0 support and private-reporting guidance.
- `CODE_OF_CONDUCT.md`: participation standards and moderation process.
- `SUPPORT.md`: documentation, bug reports, and feature requests.
- `.github/ISSUE_TEMPLATE/`: bug and feature forms.
- `.github/PULL_REQUEST_TEMPLATE.md`: review and verification checklist.

GitHub can apply these files as organization defaults once this repository
is public. Repository-specific files take precedence over the defaults.

## Community

[Contributing](https://github.com/Docleus/.github/blob/main/CONTRIBUTING.md) &middot;
[Code of conduct](https://github.com/Docleus/.github/blob/main/CODE_OF_CONDUCT.md) &middot;
[Security](https://github.com/Docleus/.github/blob/main/SECURITY.md) &middot;
[Support](https://github.com/Docleus/.github/blob/main/SUPPORT.md)

## License

[MIT](LICENSE)
