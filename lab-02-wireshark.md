# Lab 02: Network Traffic Capture & Protocol Analysis (Wireshark)

**Loom Walkthrough:** [Paste your Loom video link here after recording]

## Objective
Capture live network traffic on a macOS workstation using Wireshark, isolate DNS, TCP, and TLS protocols using display filters, and verify how domain resolution and encrypted sessions appear at the packet level.

## Environment & Prerequisites
- **Workstation:** macOS (Wi-Fi interface `en0`)
- **Tooling:** Wireshark with `ChmodBPF` capture permissions enabled
- **Network State:** Active VPN tunnel disabled during capture to inspect unencrypted local interface traffic rather than encapsulated tunnel packets

## Procedure & Verification

### 1. Live Packet Capture
1. Launched Wireshark and selected the active wireless interface (`Wi-Fi: en0`).
2. Disabled active VPN tunneling so local DNS queries and TCP/TLS handshakes were visible on `en0`.
3. Generated live network traffic and stopped the capture to inspect recorded frames.

### 2. DNS Resolution Verification
- **Display Filter:** `dns`
- **Observation:** Isolated `Standard query` and `Standard query response` packets.
- **Packet Details:** Expanded `Domain Name System (response) > Answers` and confirmed domain record resolution (CNAME/A records) for background services (`teams.events`).

### 3. TCP Three-Way Handshake Verification
- **Display Filter:** `tcp.flags.syn == 1`
- **Observation:** Confirmed initial connection setup packets displaying `[SYN]` and `[SYN, ACK]` flags in the `Info` column.

### 4. Encrypted Application Traffic (TLS) Verification
- **Display Filter:** `tls`
- **Observation:** Located `Client Hello` handshake packets and verified the target hostname via the Server Name Indication extension (`sni=imap.gmail.com`).

## Troubleshooting Notes
- **Issue:** Display filters (`dns`, `tcp`) initially returned zero packets on `Wi-Fi: en0`.
- **Root Cause:** Active VPN client encapsulated all outbound traffic into an encrypted tunnel, hiding individual protocol headers from local interface inspection.
- **Resolution:** Temporarily disconnected the VPN during capture, successfully exposing local DNS queries, TCP handshakes, and TLS SNI fields.
