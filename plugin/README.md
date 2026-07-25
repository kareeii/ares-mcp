# Ares (Claude Code plugin)

Hosted red-team toolkit for Claude Code. Install from the marketplace, then authenticate with Google in `/mcp`.

**Service:** [https://aresmcp.com](https://aresmcp.com)

## Install

```text
/plugin marketplace add kareeii/ares-mcp
/plugin install ares@ares-mcp
```

## Authenticate

1. Open `/mcp`
2. Select **ares** → **Authenticate**
3. Continue with Google on aresmcp.com
4. Status becomes **connected**

## Skills

| Skill | Use for |
|-------|---------|
| `osint` | Domain intelligence (WHOIS, DNS, certs, archives, emails) |
| `recon` | External attack surface (subdomains, live hosts, URLs) |
| `scan` | Web vulnerability assessment |
| `network` | Ports and services |
| `cloud` | Public cloud / container exposure |
| `re` | Reverse engineering / binary triage |
| `forensics` | PCAP, metadata, CTF-style analysis |

## Tools

- Lean MCP surface for day-to-day work
- Full catalog via `search_tools` → `get_tool_info` → `run_tool`
- Async jobs: `job_status`, `get_findings`, `get_artifact`
- Intrusive tools require `confirm: true`

## Links

- https://aresmcp.com
- https://aresmcp.com/docs
