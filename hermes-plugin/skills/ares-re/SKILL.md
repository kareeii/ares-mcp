---
name: ares-re
description: Operator reverse-engineering triage with Ares MCP — file type, strings, entropy, YARA, ELF/PE, disassembly, APK. Use for binary/mobile samples during an engagement or CTF. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · RE

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

- Composite: `playbook_binary_triage` / `playbook_ctf_quick`
- Static: `file_identify`, `bin_triage`, `strings_extract`, `yara_scan`, ELF/PE helpers
- Mobile: `jadx_decompile`, `android_manifest`
- Pivot strings (URLs/emails/keys) into engagement facts → osint/network/cloud
