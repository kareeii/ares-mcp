---
name: ares-ad-light
description: Light Active Directory / creds methodology with Ares MCP — SMB/LDAP enum, Kerberoast/AS-REP, capped spray. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Methodology · AD Light

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

1. `playbook_ad_enum`
2. With domain creds: `kerberoast`, `asrep_roast`
3. Capped `password_spray` only when appropriate (max 30 users)
4. `hash_identify` / `hash_crack` on captured material
5. `engagement_report`
