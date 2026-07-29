---
name: ares-network
description: Network and service recon with Ares MCP (port scans, banner grab, TLS/SSH audit, unauthenticated service checks). Use for authorized host/network testing.
category: security
mcp_server: ares
---

# Ares Network

Map ports and exposed services on authorized hosts.

## Prerequisites

The `ares` MCP server must be authenticated via OAuth in `/mcp` before use.

## Scope

- Confirm hosts/IPs (and any CIDR) are in scope.
- Start with quick profiles; widen only if needed.

## Workflow

### 1. Composite (preferred)

Use `playbook_network_sweep` via `run_tool`.

### 2. Port scanning

1. `port_scan` — `profile=quick`, `service_detect=true`
2. `naabu_scan` if a faster TCP pass helps
3. Focused/standard profiles or explicit `ports` on interesting hosts
4. `port_scan_udp` only when UDP is in scope

### 3. Fingerprint

- `banner_grab`, `ssh_audit`, `ssl_audit`, `http_probe` on open HTTP ports
- `firewall_detect`, `traceroute` when useful

### 4. Service checks

Match open ports: `ftp_enum`, `smtp_enum`, `smb_enum`, `smb_shares`, `redis_unauth_check`, `mongodb_unauth_check`, `elasticsearch_enum`, `mysql_enum`, `postgres_enum`, `rdp_check`, `vnc_check`, `snmp_enum`, `nfs_enum`, `ldap_anon_enum`.

Discover others with `search_tools` / `list_capabilities(category="scan")`.

### 5. Deliverable

- Host → open ports → service
- Confirmed exposures (ranked by severity)
- Hand-off web apps to scan, cloud control planes to cloud

## Rules

- Authorized targets only.
- No internet-wide scanning.
- Keep results compact via `get_findings`.
