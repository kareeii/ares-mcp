---
name: ares-scan
description: Operator web/app assessment with Ares MCP — crawl, fuzz, nuclei, headers, CORS, API/GraphQL, injection tests. Use when assessing a named website or API during a security engagement. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Scan

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

1. `engagement_create` with `https://…` primary target (or reuse recon engagement)
2. `playbook_web_app_test` / `playbook_vuln_triage` / `playbook_api_deep`
3. Discovery: `web_crawl`, `dir_fuzz`, `js_endpoint_extract`
4. Scanners: `nuclei_scan` (`critical_high` first)
5. Injection tools when relevant (`sqli_test`, `xss_test`, …) — server handles confirm
6. `engagement_findings` / `engagement_report`
