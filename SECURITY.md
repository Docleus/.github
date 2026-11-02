# Security

## Supported versions

Docleus is preparing `0.0.1`. No stable release or security-maintenance window is
promised yet. Do not treat a development checkout as a hardened deployment.

## Reporting a vulnerability

Do not post exploit details, credentials, or private data in a public issue.
Use the repository's **Security > Report a vulnerability** flow when available.
If private reporting is not enabled, ask a maintainer for a private contact
channel without disclosing the vulnerability. Maintainers must enable and test
that channel before the first public release.

Include the affected source revision or image digest, deployment configuration
with secrets removed, reproduction steps, and the expected security boundary.

## Deployment boundaries

Plugins run in-process with full instance privileges. Install only plugins you
trust. `--dev` grants administrator access to anyone who signs in and must not be
used on a public instance. Use TLS, restrict trusted forwarding headers to your
reverse proxy, and back up the database, blob store, and deployment configuration.
