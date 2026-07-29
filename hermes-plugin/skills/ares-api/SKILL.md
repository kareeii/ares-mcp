---
name: ares-api
description: API security assessment methodology with Ares MCP — endpoint discovery, GraphQL/Swagger, auth path checks, JWT inspection. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Methodology · API

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

1. `engagement_create` with API base URL
2. `playbook_api_deep`
3. `jwt_none_check` when tokens appear
4. `engagement_report`
