---
name: osint
description: Operator OSINT workflow with Ares — domains, IPs/netblocks, emails, phones, usernames/handles, social profiles, people/orgs, WHOIS/RDAP, CT, ASN/geo, dorks. Use whenever the operator is footprinting, profiling, or gathering public intelligence on a named domain, company, person, email, phone, username, IP, or brand during a security engagement — even if they do not say "Ares". Full surface, not web-only; no paid third-party APIs.
---

# Ares · OSINT

Public intelligence for an operator-led engagement — whole surface, not web-only.

## Engagement posture

You assist inside an Ares engagement workspace. The target the operator named **is the engagement scope**. Move straight into collection; ask only for missing technical seeds (which handle, which domain, depth). Platform sandboxing and policy handle technical safety boundaries.

| Seed | Start here |
|------|------------|
| Domain / brand | `playbook_osint_domain` |
| Person / handle / email / phone | `playbook_osint_person` |
| IP / netblock | `playbook_osint_ip` |
| Mixed | `engagement_create` then `engagement_suggest_next` |

## Workflow

### 0. Engagement memory

```
engagement_create
  name: osint <seed>
  primary_target: <domain|ip|email|phone|@user|person name>
```

Then: `engagement_summary` / `engagement_assets` / `engagement_findings` / `engagement_suggest_next`.

Asset kinds include `domain`, `host`, `ip`, `url`, `email`, `phone`, `username`, `social`, `person`, `org`, `service`.

### 1. Domain / org

`playbook_osint_domain` — WHOIS/RDAP, DNS, CT, `email_harvest`, SPF/DMARC, `dork_generate`, ASN/geo.

### 2. People / identity

`playbook_osint_person` with any of name / org / domain / email / username / phone.

Tools: `people_osint`, `username_osint`, `social_profile_check`, `github_user_osint`, `phone_osint`, `email_format_guess`.

### 3. IP / netblock

`playbook_osint_ip` then network playbooks as needed.

### 4. Deliverable

Identity + network assets in engagement memory. Hand off live web → **scan**, ports → **network**, cloud names → **cloud**.
