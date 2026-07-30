# eXcap Architecture

## Overview

eXcap separates capture, decoding, state, and presentation so packet handling remains independent of Android UI lifecycle changes.

```text
Android application traffic
  → VpnService TUN (standard mode) or selected interface (root mode)
  → native capture loop
  → zdtun flow tracking / forwarding
  → nDPI protocol classification
  → connection and payload models
  → Android activities/fragments and exporters
```

## Main components

| Component | Responsibility |
|---|---|
| `CaptureService` | Foreground lifecycle, local VPN setup, capture configuration, notification, native-engine coordination |
| `CaptureHelper` | VPN consent and capture start orchestration |
| `CaptureCtrl` | External control API with package/signature checks |
| Native `capture` module | Packet ingestion, forwarding, flow state, DNS/HTTP/TLS metadata, filtering, dump generation |
| `zdtun` submodule | User-space TCP/UDP connection tracking and VPN forwarding primitives |
| `nDPI` submodule | Application-protocol detection |
| `ConnectionsRegister` | In-memory connection and payload state exposed to the UI |
| `AppsResolver` | Android UID/package attribution and app metadata |
| `StatusFragment` | Capture mode, per-app target selection, start/stop status, recent capture |
| `ConnectionsFragment` | Live and historical flow list, search, sort, filtering |
| `ConnectionDetailsActivity` | Flow metadata, payload text/hex, HTTP inspection, action controls |
| `PcapDumper` / `HarWriter` / CSV writers | Explicit user exports |

## Per-app filtering

For no-root captures, eXcap resolves selected packages and configures the VPN/app filter so capture scope can be reduced to one app or a chosen set. UID attribution maps observed flows back to installed packages. Android system limitations and shared UIDs can affect attribution precision.

## HTTPS handling

The default data path does not decrypt TLS. The decoder can classify TLS and extract metadata visible outside encryption, including SNI when present and not protected by newer TLS privacy mechanisms. Optional external add-on support is isolated behind explicit settings and Android certificate installation.

## Trust boundaries

1. **Captured app → VPN interface:** untrusted packet bytes enter native parsers.
2. **Native engine → Java model:** parsed metadata and bounded payload chunks cross JNI.
3. **App sandbox → exported file:** sensitive data crosses the sandbox only after a user-selected export.
4. **App → optional collector/proxy/add-on:** data leaves the local-only path only when the user configures the feature.
5. **CI → APK artifact:** dependencies, submodules, build actions, and signing determine artifact integrity.

## Safety controls

- explicit Android VPN consent;
- foreground-service notification during capture;
- one-tap stop operation;
- per-app scope selection;
- bounded payload and connection retention preferences;
- no hidden background activation path in the standard UI;
- no default TLS interception; and
- no eXcap analytics or advertising dependency.

## Known platform constraints

- Android permits only one active VPN service for a user/profile.
- Another always-on VPN must be disabled before standard capture starts.
- Some system or work-profile traffic may be unavailable.
- Shared UIDs can map a flow to more than one package.
- Encrypted ClientHello, DNS-over-HTTPS, QUIC, certificate pinning, and application-layer encryption can reduce visible metadata.
- OEM background restrictions can terminate long-running captures despite a foreground service.
