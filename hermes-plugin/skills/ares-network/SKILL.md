---
name: ares-network
description: Operator network/service recon with Ares MCP — port scans, banner grab, TLS/SSH audit, unauthenticated service checks. Use for named host/IP/CIDR exposure mapping during a security engagement. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Network

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

1. `playbook_osint_ip` when seed is an IP
2. `playbook_network_sweep` / `port_scan` (quick → wider)
3. Fingerprint: `banner_grab`, `ssh_audit`, `ssl_audit`
4. Service enums matching open ports (SMB/LDAP/RDP/DB/Redis/…)
5. `engagement_assets(kind=service)` + hand HTTP apps to **ares-scan**
