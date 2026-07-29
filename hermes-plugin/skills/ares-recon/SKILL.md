---
name: ares-recon
description: External attack-surface mapping with Ares MCP (subdomains, live hosts, URLs, tech, TLS, subdomain takeover, optional ports). Use for mapping authorized domains.
category: security
mcp_server: ares
---

# Ares Recon

Map the external attack surface of an authorized domain.

## Prerequisites

The `ares` MCP server must be authenticated via OAuth in `/mcp` before use.

## Scope

- Confirm domain and depth (`quick` vs `standard`).
- Do not expand onto third-party systems outside scope.

## Workflow

### 1. Composite (preferred)

Use `playbook_external_attack_surface` via `run_tool`:
```
domain: <target_domain>
depth: quick|standard
include_ports: false|true
```

Alternatives: `playbook_web_recon`, `playbook_bug_bounty_recon`.

Poll `job_status`, then retrieve with `get_findings`.

### 2. Stepwise

1. `dns_lookup` / `cert_transparency`
2. `subdomain_enum` (passive first)
3. `http_probe` on discovered hosts
4. `url_enum` → `url_live_filter`
5. `web_crawl` on priority hosts
6. `tech_fingerprint`, `tls_inspect`, `cdn_detect`, `waf_detect`
7. `subdomain_takeover` on dangling candidates
8. Optional: `port_scan` (`profile=quick` first)

### 3. Deliverable

- Live hosts and notable titles/tech
- Interesting staging/admin hostnames
- TLS or takeover signals worth follow-up
- Hand-off: web vulns → scan; deep ports/services → network; public cloud → cloud

## Rules

- Authorized targets only.
- Prefer playbooks before long tool chains.
- Keep host lists capped unless the user asks for full breadth.
