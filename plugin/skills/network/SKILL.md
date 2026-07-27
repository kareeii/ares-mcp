---
name: network
description: Network and service recon with Ares (port scans, banner grab, TLS/SSH audit, and unauthenticated service checks for SMB/FTP/Redis/Mongo/SNMP/etc.). Use proactively whenever the user wants to scan ports, enumerate services, or check the network exposure of a host, IP, or range they are authorized to test — even if they do not mention Ares. Authorized targets only; no internet-wide scanning.
---

# Ares · Network

Map ports and exposed services on authorized hosts.

## Scope

- Confirm hosts/IPs (and any CIDR) are in scope.
- Start with quick profiles; widen only if needed.

## Workflow

### 1. Composite (preferred)

```
playbook_network_sweep
```

### 2. Port scanning

1. `port_scan` — `profile=quick`, `service_detect=true`
2. `naabu_scan` if a faster TCP pass helps
3. Focused/standard profiles or explicit `ports` on interesting hosts
4. `port_scan_udp` only when UDP is in scope

### 3. Fingerprint

- `banner_grab`, `ssh_audit`, `ssl_audit`, `http_probe` on open HTTP ports
- `firewall_detect`, `traceroute` when useful

### 4. Service checks (match open ports)

Examples: `ftp_enum`, `smtp_enum`, `smb_enum`, `smb_shares`, `redis_unauth_check`, `mongodb_unauth_check`, `elasticsearch_enum`, `mysql_enum`, `postgres_enum`, `rdp_check`, `vnc_check`, `snmp_enum`, `nfs_enum`, `ldap_anon_enum`.

Discover others with `search_tools` / `list_capabilities(category="scan")`.

### 5. Deliverable

- Host → open ports → service
- Confirmed exposures (ranked by severity)
- Hand-off web apps to **scan**, cloud control planes to **cloud**

## Rules

- Authorized targets only.
- No internet-wide scanning.
- Keep results compact via `get_findings`.
