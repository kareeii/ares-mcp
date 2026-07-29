---
name: ares-osint
description: Domain and org OSINT with Ares MCP (WHOIS, DNS, certificate transparency, email harvest, SPF/DMARC, tech footprint). Use proactively for domain/company footprinting on authorized targets.
category: security
mcp_server: ares
---

# Ares OSINT

Gather public intelligence on an authorized domain using the Ares MCP server.

## Prerequisites

The `ares` MCP server must be authenticated via OAuth in `/mcp` before use.

## Scope

- Confirm the target domain with the user.
- Stay on authorized assets only.

## Workflow

### 1. Composite (preferred)

Use `playbook_osint_domain` via `run_tool`:
```
domain: <target_domain>
```
Covers WHOIS, DNS, certificate transparency, public email harvest, and SPF/DMARC in one job.
Poll with `job_status`, then retrieve with `get_findings`.

### 2. Individual tools

| Goal | Tool |
|------|------|
| WHOIS / RDAP | `whois_lookup`, `rdap_lookup` |
| DNS | `dns_lookup`, `reverse_dns` |
| Mail auth | `spf_dmarc_check`, `mx_security` |
| Certificates | `cert_transparency` |
| Archives / URLs | `wayback_machine`, `url_enum` |
| Emails | `email_harvest` |
| Tech / CDN | `tech_fingerprint`, `cdn_detect`, `favicon_hash` |
| Network context | `asn_lookup`, `ip_geolocate` |
| Dork ideas | `dork_generate` |

Discover additional tools with `search_tools` / `list_capabilities`.

### 3. Results

- Prefer playbook + `job_status` → `get_findings`.
- Summarize: identity, DNS/mail posture, hostnames from CT/archives, public emails, tech hints.
- Next steps: surface map → recon; web testing → scan; ports → network.

## Rules

- Authorized targets only.
- Keep output compact; page findings instead of dumping raw artifacts.
