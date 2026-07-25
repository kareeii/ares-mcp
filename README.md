# Ares

Hosted red-team toolkit for [Claude Code](https://claude.com/claude-code).

This repository is the **marketplace install surface** only. The product runs at [aresmcp.com](https://aresmcp.com). Server source is not published here.

## Install

```text
/plugin marketplace add kareeii/ares-mcp
/plugin install ares@ares-mcp
```

Installs the MCP connector and skills: **osint**, **recon**, **scan**, **network**, **cloud**, **re**, **forensics**.

## Authenticate

1. Run `/mcp`
2. Select **ares** → **Authenticate**
3. Continue with Google on aresmcp.com
4. Status becomes **connected**

Do not put API keys or Bearer tokens in plugin config.

### Manual HTTP

```bash
claude mcp add --transport http -s user ares https://aresmcp.com/mcp
```

Authenticate via `/mcp` afterward. Skills come with the plugin install.

## Skills

| Skill | Intent | Example |
|-------|--------|---------|
| **osint** | Domain intelligence | OSINT on example.com |
| **recon** | Attack surface map | Recon example.com |
| **scan** | Web vulns | Scan https://app.example.com |
| **network** | Ports & services | Network map for in-scope hosts |
| **cloud** | Public cloud exposure | Check public buckets for acme |
| **re** | Reverse engineering | Triage this binary/APK |
| **forensics** | Evidence / CTF | Analyze this pcap |

## How it works

| | |
|--|--|
| Hosted tools | ~172 real scanners and recon tools |
| Default surface | Lean list (control + common pins + `run_tool`) |
| Discovery | `search_tools` → `get_tool_info` → `run_tool` |
| Results | Compact summary + top findings; page with `get_findings` |
| Intrusive actions | Require `confirm: true` |

### Control tools

`list_capabilities`, `search_tools`, `get_tool_info`, `run_tool`, `job_status`, `job_cancel`, `list_jobs`, `get_findings`, `get_artifact`

### Common pinned tools

`dns_lookup`, `subdomain_enum`, `http_probe`, `port_scan`, `nuclei_scan`, `dir_fuzz`, `fetch_url`, `web_crawl`, `url_enum`, `playbook_web_recon`, `playbook_external_attack_surface`, `playbook_vuln_triage`

## Categories

| Category | Focus |
|----------|--------|
| recon | DNS, subdomains, URLs, tech, public OSINT surface |
| scan | Web/network probes, nuclei, gated injection |
| cloud | Buckets, metadata, Docker/K8s, image/IaC |
| binary | File, strings, YARA, PE/ELF, JADX |
| forensics | PCAP, EXIF, decode helpers |
| playbook | Multi-step workflows |
| creds / ad | Light hash/NTLM/SSH/SMB/LDAP checks |

## Authorization

Authorized security testing and research only. You are responsible for scope and permission on every target.

## Links

- Product: https://aresmcp.com
- Docs: https://aresmcp.com/docs
- Privacy: https://aresmcp.com/privacy
- Terms: https://aresmcp.com/terms
