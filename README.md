# Ares

Hosted red-team toolkit for [Claude Code](https://claude.com/claude-code).

This repository is the **marketplace install surface** only (plugin manifests + skills). The product runs at [aresmcp.com](https://aresmcp.com). Server source is not published here.

## Install

```text
/plugin marketplace add kareeii/ares-mcp
/plugin install ares@ares-mcp
```

Installs the MCP connector plus surface and methodology skills.

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

### Surface

| Skill | Intent | Example |
|-------|--------|---------|
| **osint** | Domain / identity intelligence | OSINT on example.com or @handle |
| **recon** | Attack surface map | Recon example.com |
| **scan** | Web/app vulns | Scan https://app.example.com |
| **network** | Ports & services | Network map for in-scope hosts |
| **cloud** | Public cloud exposure | Check public buckets for acme |
| **re** | Reverse engineering | Triage this binary/APK |
| **forensics** | Evidence / CTF | Analyze this pcap |

### Methodology

| Skill | Intent |
|-------|--------|
| **web-app** | End-to-end web assessment + engagement report |
| **api** | API/GraphQL/auth path assessment |
| **ad-light** | Light AD/creds workflow |
| **external-recon** | Full external pass (`playbook_full_external`) |
| **people-osint** | Person/email/phone/username OSINT |

## How it works

| | |
|--|--|
| Hosted tools | ~200 real scanners, recon, identity, AD/API helpers |
| Default surface | Lean list (control + common pins + `run_tool`) |
| Engagement memory | `engagement_create` → tools/playbooks → `engagement_report` |
| Discovery | `search_tools` → `get_tool_info` → `run_tool` |
| Results | Compact summary + top findings; page with `get_findings` / engagement findings |
| Intrusive actions | Server auto-handles confirm for engagement invocations |

### Control tools

`list_capabilities`, `search_tools`, `get_tool_info`, `run_tool`, `job_status`, `job_cancel`, `list_jobs`, `get_findings`, `get_artifact`, plus `engagement_create` / `summary` / `assets` / `findings` / `report` / `timeline` / `suggest_next` / facts

### Common pinned tools

`dns_lookup`, `subdomain_enum`, `http_probe`, `port_scan`, `nuclei_scan`, identity OSINT pins, `playbook_full_external`, `playbook_external_attack_surface`, `playbook_vuln_triage`, `playbook_osint_*`, `playbook_api_deep`, `playbook_ad_enum`

## Categories

| Category | Focus |
|----------|--------|
| recon | DNS, subdomains, URLs, tech, identity OSINT |
| scan | Web/API/network probes, nuclei, injection |
| cloud | Buckets, metadata, Docker/K8s, image/IaC |
| binary | File, strings, YARA, PE/ELF, JADX |
| forensics | PCAP, EXIF, decode helpers |
| playbook | Multi-step + stateful composites |
| creds / ad | Hash/NTLM/SSH, SMB/LDAP, kerberoast/AS-REP, capped spray |
| control | Jobs + engagement memory |

## Operator posture

Ares is built for **operator-led security engagements**. The named target defines session scope; the agent is the execution partner. Platform policy still blocks private/metadata/self targets.

## Links

- Product: https://aresmcp.com
- Docs: https://aresmcp.com/docs
- Privacy: https://aresmcp.com/privacy
- Terms: https://aresmcp.com/terms
