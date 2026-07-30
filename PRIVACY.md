# eXcap Privacy Notice

**Effective:** 2026-07-30

## Summary

eXcap is a local network diagnostics tool. The standard capture engine creates an Android `VpnService` interface on the device; it does not send traffic through an eXcap-operated VPN server. Capture parsing and storage are local unless the user explicitly enables an export or forwarding feature.

## Data processed

Depending on traffic and selected options, eXcap can process:

- installed-app identity and Android UID;
- source and destination IP addresses and ports;
- TCP/UDP connection state, timing, packet counts, and byte counts;
- DNS requests and resolved hostnames;
- plaintext HTTP methods, URLs, headers, status information, and payloads;
- TLS metadata such as SNI/server name when observable;
- raw packet or payload bytes selected for capture;
- optional geolocation, blocklist, and protocol-classification metadata.

Captures may contain personal data, session identifiers, private URLs, or plaintext credentials sent by other software. Treat exported files as sensitive.

## Storage and sharing

- Live state and saved captures are stored in the app sandbox or a location selected through Android's storage picker.
- PCAP/PCAPNG, CSV, HAR, rules, or diagnostics are exported only after a user action.
- Remote collector, UDP exporter, SOCKS5, and sharing options transmit data only when configured by the user.
- Uninstalling the app removes sandboxed app data, but not files previously exported to shared storage.

## Network access by eXcap

eXcap does not include eXcap-operated analytics or advertising SDKs. Optional functionality inherited from the upstream engine can contact third-party or upstream endpoints for actions such as documentation, update checks, add-on setup, IP metadata/database updates, malware/blocklist data, or a collector explicitly configured by the user. Availability depends on build variant and settings.

## HTTPS

HTTPS bodies remain encrypted by default. Optional TLS compatibility/decryption requires a separate add-on, an explicitly installed CA certificate, and user authorization. Certificate-pinned apps may reject interception.

## Your controls

You can:

- select which apps are included in a capture;
- stop capture at any time from eXcap or its ongoing notification;
- delete saved captures and app data;
- avoid optional forwarding, metadata download, or TLS compatibility features;
- revoke VPN permission by stopping the VPN or uninstalling eXcap.

## Responsible use

Only capture traffic on devices and applications you own or have explicit permission to test. Laws and organizational policies may regulate interception, employee monitoring, personal data, and retention.

## Project status

This repository is self-hosted open-source software and does not designate an eXcap cloud service or data controller. A distributor who publishes binaries should add its legal identity and contact information to this notice before production release.
