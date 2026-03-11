# NetWatch Signature Feed

Open-source threat signature feed for LLM infrastructure protection.

## Overview

This repository contains machine-readable threat signatures designed to detect and block malicious activity targeting LLM endpoints. Signatures are organized into three layers:

- **Layer 1 (Network):** Header fingerprints, user-agent patterns, and behavioral path-scanning rules
- **Layer 2 (Exploit):** Payload-level exploit patterns targeting LLM frameworks
- **Layer 3 (Prompt):** Prompt injection and jailbreak detection patterns

## Consumer

These signatures are consumed by [Blackwall](https://github.com/NetWatchReport/blackwall), a reverse proxy purpose-built for protecting self-hosted LLM infrastructure. Blackwall pulls this feed on a configurable interval and applies signatures without requiring restarts.

## Format

All signature data is stored as JSON. The `manifest.json` file contains SHA-256 hashes for each data file, allowing consumers to verify integrity before applying updates.

```
manifest.json       Version metadata and file hashes
ips.txt             Known malicious IPs (one per line)
signatures.json     Layer 1 network detection signatures
exploits.json       Layer 2 exploit detection patterns
prompts.json        Layer 3 prompt injection patterns
```

## Update Cadence

Signatures are updated as new threats are documented and verified. Each update increments the version in `manifest.json` and is tagged as a release.

## Privacy

This is a one-way feed. Consuming this data sends nothing back to NetWatch. Blackwall fetches signature files over HTTPS from this repository. No telemetry, no callbacks, no registration.

## Advisories

Detailed write-ups for each signature are published in the [advisories repository](https://github.com/NetWatchReport/advisories).

## Contact

Report threats or false positives: abuse@netwatch.report

## License

MIT
