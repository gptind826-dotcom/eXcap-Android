# Security Policy

## Supported versions

| Version | Security updates |
|---|---|
| 1.x | Supported on the current main branch |
| Older/upstream snapshots | Not supported by the eXcap project |

## Reporting a vulnerability

Do **not** include packet captures, credentials, private keys, access tokens, or personal data in a public issue.

Use GitHub's **Private vulnerability reporting** feature for this repository when available. Include:

- affected commit or version;
- Android version and device architecture;
- clear reproduction steps using synthetic/non-sensitive traffic;
- expected and actual behavior;
- impact assessment; and
- a minimal proof of concept, if safe.

If private reporting has not been enabled by the repository owner, open a public issue containing only a request for a private contact channel—no vulnerability details.

## Scope priorities

High-priority reports include:

- capture data escaping the app without an explicit user configuration;
- VPN bypass or traffic corruption caused by the capture engine;
- exported-file path traversal or unintended file disclosure;
- privilege, UID-attribution, or app-filter isolation failures;
- unsafe handling of TLS add-on IPC or certificates;
- memory-safety defects in native packet parsing; and
- dependency or CI compromise affecting produced APKs.

## Build integrity

- GitHub Actions pins the Android, NDK, CMake, and Java major versions.
- Every CI APK artifact receives a SHA-256 checksum.
- Debug artifacts are debug-signed and must not be represented as production releases.
- Release keystores and passwords must never be committed. Use protected GitHub Environment secrets and require reviewer approval for production signing.
