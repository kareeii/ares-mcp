---
name: ares-external-recon
description: Full external attack-surface methodology with Ares MCP — OSINT, surface, nuclei via playbook_full_external, engagement report. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Methodology · External Recon

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

1. `engagement_create` with domain
2. `playbook_full_external` (OSINT → surface → nuclei on memory URLs)
3. Optional ports / identity pivots
4. `engagement_timeline` + `engagement_report`
