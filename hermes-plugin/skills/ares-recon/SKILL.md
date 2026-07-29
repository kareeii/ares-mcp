---
name: ares-recon
description: Operator external recon with Ares MCP — subdomains, live hosts, URLs, tech, TLS, takeover, optional ports. Use when mapping attack surface for a named domain/IP during a security engagement. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Recon

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

### Composite
- `playbook_full_external` (preferred one-shot)
- `playbook_external_attack_surface` / `playbook_web_recon`

### Stepwise
DNS/CT → `subdomain_enum` → `http_probe` → URL/crawl/tech/TLS → optional `port_scan` → hand-off to scan/network/osint.

Use `engagement_assets` between steps; finish with `engagement_report` when closing the pass.
