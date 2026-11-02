# Contributing to Docleus

Start with the [online documentation](https://docleus.io) and the README of the
repository you want to change. Participation follows the
[code of conduct](CODE_OF_CONDUCT.md); report vulnerabilities through
[SECURITY.md](SECURITY.md).

Discuss substantial or cross-repository changes in an issue before implementing
them. Keep changes focused, with regression tests for bugs and tests for new
behavior. Do not include credentials, local data, build output, or unrelated
formatting changes.

## Source setup

Use Node.js 24 and pnpm 11.21.0. Clone `docleus-core`, `docleus`,
`docleus-plugin-template`, and the official plugin repositories into one parent
directory, using their repository names. Install core first, then each sibling:

```sh
pnpm install --frozen-lockfile
pnpm check
```

Each repository has its own lockfile. There is no root pnpm workspace.
`@docleus/*` packages remain private; the `link:` dependencies refer to the
sibling sources. Do not replace them with unpublished npm versions.

## Implementation

Write code, comments, tests, and documentation in English. Use strict TypeScript,
ESM, named exports, and public package entry points. Plugins depend on the public
SDK, not core internals or another plugin's implementation. Register resources
through `ctx` so unloading a plugin removes them. Public exports need TSDoc;
extension points include dispatch mode and experimental stability.

Ask before adding runtime dependencies or changing a public SDK contract. Use
exact dependency versions and permissive licenses. Never modify vendored code
directly. Update the owning README when changing behavior or a public API.

## Verification

Run `pnpm check` in every changed repository. Core and plugin checks cover types,
lint, formatting, import boundaries, licenses, and unit/in-process integration
tests. The distribution runs its Node tests. A public core/SDK change also needs
every plugin's checks.

Run `pnpm build` and, where present, `pnpm e2e`; install Chromium once with
`pnpm exec playwright install chromium`. Postgres, real S3, Dex, and Docker smoke
tests need external services and are separate gates. Report failures and missing
coverage explicitly; do not add retries or weaken assertions.

Use Angular-style commit subjects, such as `fix(editor): keep moved pages visible`.
A cross-repository change identifies the related repositories in each commit
body. Maintainers review the complete source set before tagging a release.
