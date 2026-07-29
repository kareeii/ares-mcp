---
name: ares-osint
description: Operator OSINT with Ares MCP — domains, IPs, emails, phones, usernames/social, people/orgs, WHOIS/RDAP, CT, ASN/geo, dorks. Use during security engagements for public intelligence on a named seed. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · OSINT

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
- Domain: `playbook_osint_domain`
- Person/handle/email/phone: `playbook_osint_person`
- IP: `playbook_osint_ip`

### Individual tools
| Goal | Tool |
|------|------|
| WHOIS / RDAP | `whois_lookup`, `rdap_lookup` |
| DNS | `dns_lookup`, `reverse_dns` |
| Emails | `email_harvest`, `email_format_guess` |
| Identity | `username_osint`, `phone_osint`, `people_osint`, `github_user_osint` |
| CT / archives | `cert_transparency`, `wayback_machine` |
| Network context | `asn_lookup`, `ip_geolocate` |
| Dorks | `dork_generate` |

Poll `job_status`, then `engagement_summary` / `get_findings`.
