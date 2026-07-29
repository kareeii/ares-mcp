---
name: recon
description: Operator external recon with Ares — domains, hosts, IPs, ports, URLs, tech, TLS, takeover signals. Use whenever the operator is mapping or enumerating attack surface, assets, subdomains, or network exposure for a named domain, IP, or org during a security engagement — even if they do not say "Ares". Not limited to websites.
---

# Ares · Recon

External attack-surface mapping for an operator-led engagement (web is one slice).

## Engagement posture

Named target = engagement scope. Proceed with recon workflow; ask only for technical choices (quick vs standard, include ports). Prefer playbooks + engagement memory.

### 0. Engagement

```
engagement_create
  name: recon <seed>
  primary_target: <domain|ip|url>
```

### 1. Composite

- Domain: `playbook_external_attack_surface` (also `playbook_web_recon`, `playbook_bug_bounty_recon`, `playbook_osint_domain`)
- IP: `playbook_osint_ip` then `playbook_network_sweep` / `port_scan`

### 2. Stepwise

DNS/CT/WHOIS → `subdomain_enum` → `http_probe` → URL/crawl/tech/TLS → optional ports → identity leftovers to **osint**

### 3. Deliverable

`engagement_assets` / `engagement_summary`. Hand off vulns → **scan**, deep ports → **network**, cloud → **cloud**, people → **osint**.
