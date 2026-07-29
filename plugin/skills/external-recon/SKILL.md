---
name: external-recon
description: Operator methodology for full external attack-surface assessment with Ares — OSINT, subdomains, HTTP, ports, nuclei, engagement report. Use when the operator wants an end-to-end external pass on a domain during a security engagement.
---

# Ares · Methodology · External Recon

## Workflow
1. `engagement_create` with domain
2. Prefer `playbook_full_external` (OSINT → surface → nuclei on memory URLs)
   - Or stepwise: `playbook_osint_domain` → `playbook_external_attack_surface` → `playbook_vuln_triage`
3. Optional ports: `include_ports=true` or `playbook_network_sweep`
4. Identity leftovers → **osint** / **people-osint**
5. `engagement_timeline` + `engagement_report`

## Deliverable
Assets by kind, deduped findings, attack paths, next steps.
