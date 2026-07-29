---
name: ares-people-osint
description: People/identity OSINT methodology with Ares MCP — person/org, username/social, phone/email, GitHub, engagement memory. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Methodology · People OSINT

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

1. `engagement_create` with person/email/phone/@user
2. `playbook_osint_person`
3. Expand username/GitHub/phone/email tools
4. Pivot discovered domains → **ares-external-recon**
5. `engagement_report`
