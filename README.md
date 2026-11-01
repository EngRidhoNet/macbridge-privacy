# MacBridge Privacy Policy

**Last Updated:** November 2026  
**Effective Date:** November 1, 2026

MacBridge ("we", "our", or "the application") is a native, privacy-focused remote desktop application designed for macOS and iPadOS. We believe that your desktop, your keystrokes, your screen content, and your network topology belong exclusively to you. 

MacBridge is built from the ground up on a **zero-telemetry, zero-cloud, privacy-first architecture**.

---

## 1. Core Principles

1. **No Data Collection:** We do not collect, harvest, aggregate, sell, or rent any personal data, usage metrics, or diagnostic telemetry.
2. **No Accounts or Cloud Storage:** MacBridge operates without user accounts, cloud sign-ins, centralized databases, or relay servers operated by MacBridge.
3. **No Third-Party Analytics or Advertising:** The application contains zero advertising SDKs, third-party analytics trackers, crash reporters, or behavioral monitors.
4. **End-to-End Local and Direct Cryptography:** All network communication—whether local over Bonjour or remote over peer-to-peer tunnels—is secured with Mutual TLS 1.3 (mTLS) with pinned cryptographic certificates and ephemeral session keys.

---

## 2. Information Handled by the Application

### A. Screen Capture and Desktop Video
- **Host (macOS):** When an authenticated session is active, macOS `ScreenCaptureKit` captures display frames in memory. Frames are encoded in hardware using `VideoToolbox` (H.264) and sent directly over the authenticated mTLS socket.
- **Client (iPadOS):** Video packets are decoded and displayed in memory via `AVSampleBufferDisplayLayer`.
- **Retention:** Video frames and desktop audio are streamed transiently in real time. They are never cached to disk, recorded, or transmitted to any third party.

### B. Keyboard, Mouse, and Trackpad Input
- **Client (iPadOS):** Hardware keyboard, trackpad, mouse, and touchscreen inputs are captured via public iPadOS UIKit APIs, normalized into device-agnostic protocols, and transmitted over the encrypted connection.
- **Host (macOS):** Normalized events are injected into the macOS window server via Quartz Event Services.
- **Retention:** Keystrokes, mouse clicks, and coordinates exist only in volatile memory for the duration of the stream. They are never logged, stored, or analyzed.

### C. Device Cryptographic Identities
- Each device generates a persistent 256-bit cryptographic identity (Ed25519 / P-256) locally upon initial launch.
- Private keys never leave the device. They are stored securely in the hardware Secure Enclave or the platform Keychain (`kSecClassKey`).
- Public keys and SHA-256 fingerprints are exchanged solely during explicit user-approved pairing.

### D. Network Endpoints & Wake Credentials
- Local IP addresses, MAC addresses, and user-configured remote DNS endpoints (e.g. Tailscale or WireGuard private hostnames) are stored strictly on your local device.
- Wake-on-LAN Magic Packets and optional authenticated wake tickets are generated locally and transmitted directly to the configured targets.

---

## 3. Apple Privacy Manifest (NSPrivacy) Declarations

In compliance with Apple's privacy manifest requirements (`PrivacyInfo.xcprivacy`), MacBridge declares:

### Zero Tracking
`NSPrivacyTracking`: `false`  
MacBridge does not track users across apps and websites owned by other companies.

### Zero Tracking Domains
`NSPrivacyTrackingDomains`: `[]`

### Required Reason API Declarations
MacBridge accesses platform APIs solely for declared, sanctioned purposes:

1. **`NSPrivacyAccessedAPITypeUserDefaults` (Reason: `CA92.1`)**
   - Accessed to read and write app-specific preferences and state within the app sandbox (e.g., paired device display names, letterboxing preferences, wake timeout intervals, and pointer sensitivity settings).
2. **`NSPrivacyAccessedAPITypeSystemBootTime` (Reason: `35F9.1`)**
   - Accessed to measure local monotonic uptime and elapsed time across wake intervals, session heartbeats, and retransmission backoffs. Does not identify the device or track users.

---

## 4. In-App Purchases & StoreKit 2

- MacBridge offers an optional lifetime unlock for advanced remote access features.
- All transactions are handled exclusively through Apple's native **StoreKit 2** framework.
- Apple processes your payment information and transaction receipts under the standard Apple Media Services Terms and Conditions.
- MacBridge does not collect payment details, credit card numbers, billing addresses, or user identifiers.
- Entitlement status is verified cryptographically on-device using Apple's signed JWS transaction tokens.

---

## 5. System Permissions

MacBridge requests only the minimum platform permissions necessary to function:
- **macOS Screen Recording:** Required by Apple to capture the desktop display via `ScreenCaptureKit`.
- **macOS Accessibility:** Required to inject keyboard, mouse, and trackpad events into the desktop session.
- **iPadOS Local Network:** Required by Apple to discover nearby Macs via Bonjour (`_macbridge._tcp`) and connect directly.

You may revoke any permission at any time through macOS System Settings or iPadOS Settings.

---

## 6. Security & Cryptographic Verification

MacBridge enforces strict on-device security. Every cryptographic routine, certificate verification, and privacy boundary is enforced locally using Apple platform frameworks:
- Support & Questions: contact@macbridge.io

---

## 7. Contact Information

If you have questions, concerns, or security disclosures regarding this Privacy Policy, please contact:
- **Email:** security@macbridge.io
- **GitHub Issues:** [https://github.com/macbridge/macbridge/issues](https://github.com/macbridge/macbridge/issues)
