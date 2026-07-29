---
name: ares-forensics
description: Operator light forensics/CTF with Ares MCP — PCAP, EXIF/GPS, entropy, decode/cipher helpers. Use for evidence artifacts during an engagement or CTF. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Forensics

## Prerequisites

1. `ares` is configured in `~/.hermes/config.yaml` with `url: https://aresmcp.com/mcp` and `auth: oauth`.
2. Authenticate once with Hermes (not Claude Code):

```bash
hermes mcp login ares
hermes mcp test ares
```

Tokens are cached under `~/.hermes/mcp-tokens/`. There is no `/mcp` Authenticate UI in Hermes.

## Engagement posture

Named target = engagement scope for this session. Prefer `engagement_create` then playbooks; close with `engagement_report` when useful.

## Workflow

- Composite: `playbook_forensics_triage` / `playbook_ctf_quick`
- PCAP: `pcap_analyze`, `pcap_dns_extract`, `pcap_http_extract`
- Meta: `exif_gps`, `exiftool_meta`
- Blobs: `file_identify`, `strings_extract`, `entropy_analyze`, `base_decode`, `xor_bruteforce`
