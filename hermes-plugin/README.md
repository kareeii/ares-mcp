# Ares MCP — Hermes Plugin

Hosted red-team toolkit for Hermes Agent. This is the **Hermes plugin surface** — the MCP server runs at [aresmcp.com](https://aresmcp.com).

## Install

1. Add MCP server to `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  ares:
    auth: oauth
    enabled: true
    url: https://aresmcp.com/mcp
```

2. Restart Hermes gateway.

3. In a new session, run `/mcp` → select **ares** → **Authenticate**.

4. Complete Google OAuth on aresmcp.com.

## Skills

Copy the `skills/` directory to `~/.hermes/skills/`, or copy individual skill folders:

| Skill | Intent | Example |
|-------|--------|---------|
| **ares-osint** | Domain intelligence | OSINT on example.com |
| **ares-recon** | Attack surface map | Recon example.com |
| **ares-scan** | Web vulns | Scan https://app.example.com |
| **ares-network** | Ports & services | Network map for in-scope hosts |
| **ares-cloud** | Public cloud exposure | Check public buckets for acme |
| **ares-re** | Reverse engineering | Triage this binary/APK |
| **ares-forensics** | Evidence / CTF | Analyze this pcap |

## MCP Tools

The Ares MCP server exposes ~172 red-team tools accessible via standard MCP protocol. Key control tools:

- `list_capabilities`, `search_tools`, `get_tool_info`, `run_tool`
- `job_status`, `job_cancel`, `list_jobs`, `get_findings`, `get_artifact`

Common pinned tools: `dns_lookup`, `subdomain_enum`, `http_probe`, `port_scan`, `nuclei_scan`, `dir_fuzz`, `fetch_url`, `web_crawl`, `url_enum`.

## Authorisation

Authorized security testing and research only. You are responsible for scope and permission on every target.

## Links

- Product: https://aresmcp.com
- Docs: https://aresmcp.com/docs
