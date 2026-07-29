---
name: people-osint
description: Operator methodology for people/identity OSINT with Ares — person/org seeds, username/social, phone/email, GitHub, engagement memory. Use when the engagement starts from a person, handle, email, or phone rather than only a domain.
---

# Ares · Methodology · People OSINT

## Workflow
1. `engagement_create` with person/email/phone/@user
2. `playbook_osint_person`
3. Expand: `username_osint`, `github_user_osint`, `phone_osint`, `email_format_guess`, `email_harvest` on discovered domains
4. Pivot domains → **external-recon**
5. `engagement_report`

## Notes
No paid breach/people-search APIs. Public sources + dorks only.
