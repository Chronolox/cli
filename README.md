<div align="center">

<a href="https://chronolox.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/chronolox-logo-dark.png">
    <img src="assets/chronolox-logo-light.png" alt="Chronolox — hourglass emblem and wordmark" width="360">
  </picture>
</a>

</div>

# Chronolox CLI — Command-Line Interface

This repository hosts official, pre-compiled binary distributions, release signatures, and integrity verification materials for **Chronolox CLI** (`chronolox-cli`).

Chronolox CLI is the cross-platform command-line utility for developers, creators, and operators: creating, updating, inspecting, and notarizing time-locked secrets, managing autonomous capsules (`.clox`), and validating time-lock cryptographic guarantees.

All builds are compiled with zero dynamic library dependencies and cross-platform targets (Linux, macOS, Windows) using reproducible build flags. Pre-built binaries are available on the [Releases](https://github.com/Chronolox/cli/releases) page.

---

## Capabilities

- **Time-Locked Encryption:** Encrypt payloads bound to autonomous on-chain smart contracts and threshold cryptography networks (drand / Oasis Sapphire TEE).
- **Capsule Management:** Create, inspect, seal, and verify multi-layer `.clox` capsule archives.
- **On-Chain Notary:** Anchor and verify cryptographic proofs of secret existence and timestamping.
- **Failsafe Verification:** Inspect embedded archival failsafe escrows and evaluate emergency unlock conditions.

---

## Release Verification Keys

All official binaries are cryptographically signed before release. Never execute binaries whose SHA-256 digests or GPG signatures do not match the published records.

### Public Signing Keys

- **Release Signing GPG Key ID:** `0xF873EA8F770A9136`
- **Key Fingerprint:** `CE23 439F 2EA0 9A0C 445A  F720 F873 EA8F 770A 9136`
- **User ID:** `Chronolox APT Signing Key <apt@chronolox.com>`
- **Public Key File:** Included in repository root as [`chronolox-release-key.pub`](./chronolox-release-key.pub) — always verify the fingerprint above after importing; trust the fingerprint, not the transport.

Import the key and verify a release:

```bash
gpg --import chronolox-release-key.pub
gpg --fingerprint 0xF873EA8F770A9136          # must match the fingerprint above
gpg --verify SHA256SUMS.sig SHA256SUMS        # against a release's checksum ledger
sha256sum --check SHA256SUMS --ignore-missing
```

---

## Integrity & Authenticity Verification

Each release on GitHub includes:

1. The platform binary archive (`.tar.gz` or `.zip`)
2. `SHA256SUMS` (Plaintext hash ledger)
3. `SHA256SUMS.sig` (Detached GPG signature of the hash ledger)

### 1. Verify Checksum Ledger Signature

Verify that the checksum ledger itself has not been tampered with:

```bash
gpg --verify SHA256SUMS.sig SHA256SUMS
```

*Expected output:* `gpg: Good signature from "Chronolox APT Signing Key <apt@chronolox.com>"`

### 2. Verify Binary Integrity

Run the checksum check against your downloaded archive:

#### Linux / macOS

```bash
sha256sum --check SHA256SUMS --ignore-missing
```

#### Windows (PowerShell)

```powershell
Get-FileHash -Algorithm SHA256 .\chronolox-cli-windows-amd64.zip
# Compare output manually against SHA256SUMS entry
```

---

## Installation & Execution Notes

### Linux (`amd64` / `arm64`)

```bash
tar -xzf chronolox-cli-linux-amd64.tar.gz
chmod +x chronolox-cli
./chronolox-cli --help
```

> **Note for Debian/Ubuntu Users:** An official `.deb` package is available for native installation via `sudo apt install ./chronolox-cli_*_amd64.deb`.

### macOS (`arm64` / Apple Silicon & `amd64` / Intel)

Due to macOS Gatekeeper quarantine flags on direct binary downloads, verify and strip the quarantine attribute:

```bash
tar -xzf chronolox-cli-darwin-arm64.tar.gz
xattr -d com.apple.quarantine chronolox-cli
chmod +x chronolox-cli
./chronolox-cli --help
```

### Windows (`amd64`)

Extract the `.zip` archive. Run `chronolox-cli.exe` directly from PowerShell or Command Prompt. No system drivers or registry modifications are required.

---

## Archival Failsafe Verification

Official release builds contain an embedded, encrypted source snapshot (`source_archive.7z`) protected by an autonomous on-chain time-lock escrow.

To inspect the embedded archive parameters without extracting:

```bash
./chronolox-cli failsafe status
```

To extract the codebase when the network emergency unlock timestamp has passed:

```bash
./chronolox-cli extract-source --secret-id <PUBLIC_ESCROW_SECRET_ID>
```

For complete technical specifications on the autonomous escrow design, consult the [Chronolox Architecture & Security Model](https://github.com/Chronolox/specs).

---

## Security & Bug Reporting

If you observe a checksum mismatch, corrupted binary artifact, or unexpected network behavior:

* **Do NOT file a public issue or pull request for security vulnerabilities.**
* Review our disclosure procedure in [`SECURITY.md`](./SECURITY.md).
* Contact our engineering security desk directly at **`security@chronolox.com`**.

---

## Contributing

To report packaging bugs, operating system compatibility issues, or hash verification errors, please see [`CONTRIBUTING.md`](./CONTRIBUTING.md).

---

## License

The binary releases and verification materials in this repository are distributed under the [Chronolox Binary Release License](./LICENSE).

Source code for the underlying applications is protected during commercial beta by the on-chain Cryptographic Source Escrow Failsafe documented in [`specs`](https://github.com/Chronolox/specs).
