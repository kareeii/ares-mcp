---
name: recon
description: External attack-surface mapping with Ares (subdomains, live hosts, URLs, tech, TLS, subdomain takeover, optional ports). Use proactively whenever the user wants to map, enumerate, or discover the attack surface, assets, or subdomains of a domain or target they are authorized to test — even if they do not mention Ares. Authorized targets only.
---

# Ares · Recon

Map the external attack surface of an authorized domain.

## Scope

- Confirm domain and depth (`quick` vs `standard`).
- Do not expand onto third-party systems outside scope.

## Workflow

### 1. Composite (preferred)

```
playbook_external_attack_surface
  domain: <domain>
  depth: quick|standard
  include_ports: false|true
```

Alternatives: `playbook_web_recon`, `playbook_bug_bounty_recon`.

Poll `job_status`, then `get_findings`.

### 2. Stepwise (when more control is needed)

1. `dns_lookup` / `cert_transparency`
2. `subdomain_enum` (passive first)
3. `http_probe` on discovered hosts
4. `url_enum` → `url_live_filter`
5. `web_crawl` on priority hosts
6. `tech_fingerprint`, `tls_inspect`, `cdn_detect`, `waf_detect`
7. `subdomain_takeover` on dangling candidates
8. Optional: `port_scan` (`profile=quick` first)

Use `search_tools` / `get_tool_info` / `run_tool` for anything not pinned.

### 3. Deliverable

- Live hosts and notable titles/tech
- Interesting staging/admin hostnames
- TLS or takeover signals worth follow-up
- Hand-off: web vulns → **scan**; deep ports/services → **network**; public cloud names → **cloud**

## Rules

- Authorized targets only.
- Prefer playbooks before long tool chains.
- Keep host lists capped unless the user asks for full breadth.
