# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in Chronolox official release binaries (`chronolox-heir`, `chronolox-cli`, `secret-maker`), release verification keys, or checksum infrastructure, please report it privately.

**Do NOT report vulnerabilities through public GitHub issues, discussions, or pull requests.**

### How to Report Privately

1. **Email:** Send your report to **`security@chronolox.com`**.
2. **GitHub Private Vulnerability Reporting:** You can also use GitHub's private vulnerability reporting feature under the **Security** tab of this repository.

### What to Include

- Detailed description of the observed issue (e.g. binary corruption, signature verification failure, buffer issue).
- Binary name, exact version tag, platform architecture (e.g. Linux amd64, macOS arm64).
- Computed SHA-256 hash vs published `SHA256SUMS`.
- Reproduction steps or proof-of-concept.

### Response Commitment

- Initial acknowledgment within 48 hours.
- Rapid assessment and binary revocation/re-signing if needed.
- Coordinated public disclosure once verified.
