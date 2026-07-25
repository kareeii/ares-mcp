---
name: osint
description: Domain OSINT with Ares — WHOIS, DNS, certificates, archives, public emails, tech footprint.
---

# Ares · OSINT

Gather public intelligence on an authorized domain.

## Scope

- Confirm the target domain with the user.
- Stay on authorized assets only.

## Workflow

### 1. Composite (preferred)

```
playbook_osint_domain
  domain: <domain>
```

Covers WHOIS, DNS, certificate transparency, public email harvest, and SPF/DMARC.

### 2. Expand as needed

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

### 3. Results

- Prefer playbook + `job_status` → `get_findings`.
- Summarize: identity, DNS/mail posture, hostnames from CT/archives, public emails, tech hints.
- Next steps: surface map → recon; web testing → scan; ports → network.

## Rules

- Authorized targets only.
- Keep output compact; page findings instead of dumping raw artifacts.
