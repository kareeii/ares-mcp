---
name: network
description: Operator network/service recon with Ares — port scans, banner grab, TLS/SSH audit, unauthenticated checks (SMB/FTP/Redis/Mongo/SNMP/LDAP/RDP/…), IP/ASN context. Use whenever the operator is scanning ports or enumerating services on a named host, IP, or CIDR during a security engagement — even if they do not say "Ares". Not limited to HTTP; avoid unscoped internet-wide sweeps.
---

# Ares · Network

Ports and exposed services for an operator-led engagement.

## Engagement posture

Named host/IP/CIDR = engagement scope. Run the network workflow; ask only for profile/depth. Do not run aimless internet-wide sweeps with no target.

### 0. Engagement

```
engagement_create
  name: network <ip-or-host>
  primary_target: <ip|host>
```

Or reuse recon engagement + `engagement_assets(kind="ip"|"host"|"service")`.

### 1. Composite

`playbook_network_sweep` · IP context via `playbook_osint_ip`

### 2. Ports / fingerprint / services

`port_scan` (quick → wider) · `naabu_scan` / `masscan_scan` · `banner_grab` · `ssh_audit` / `ssl_audit` · service enums matching open ports

### 3. Deliverable

Service table in engagement memory; HTTP apps → **scan**.
