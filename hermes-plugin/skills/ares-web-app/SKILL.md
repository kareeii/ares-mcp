---
name: ares-web-app
description: End-to-end web application assessment methodology with Ares MCP and engagement report. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Methodology · Web App

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

1. `engagement_create`
2. Surface: `playbook_web_recon` / crawl / `dir_fuzz`
3. Triage: `playbook_vuln_triage` (stateful — uses memory URLs)
4. Config/auth checks + injection as needed
5. `engagement_report`
