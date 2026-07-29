---
name: ad-light
description: Operator methodology for light Active Directory / creds assessment with Ares — SMB/LDAP enum, Kerberoast/AS-REP, capped password spray. Use when the operator is assessing a domain controller or AD-adjacent host during an authorized internal/engagement lab scenario.
---

# Ares · Methodology · AD Light

## Workflow
1. `engagement_create` with DC IP / domain
2. `playbook_ad_enum` (SMB/LDAP/NTLM/user enum)
3. With domain creds: `kerberoast`, `asrep_roast`
4. Capped spray only when appropriate: `password_spray` (max 30 users, single password)
5. `hash_identify` / `hash_crack` on captured material
6. `engagement_report`

## Notes
Intrusive tools auto-confirm on server. Keep user lists small. No BloodHound enterprise APIs.
