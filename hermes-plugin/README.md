# Ares MCP — Hermes Agent

Hosted red-team toolkit for [Hermes Agent](https://hermes-agent.nousresearch.com).  
The MCP server runs at [aresmcp.com](https://aresmcp.com). This folder is the **Hermes install surface** (manifest + skills).

Hermes does **not** use Claude Code’s `/mcp` UI. Auth is Hermes-native: config + `hermes mcp login`.

## 1. Add the MCP server

Edit `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  ares:
    url: "https://aresmcp.com/mcp"
    auth: oauth
    enabled: true
    # Optional: raise if long scans time out on the client side
    timeout: 300
    connect_timeout: 60
```

Notes:

- `auth: oauth` is required for the hosted product (Google sign-in via aresmcp.com).
- Do **not** put a static Bearer token in config unless you intentionally use a dashboard-minted JWT / operator key.
- Endpoint must include the `/mcp` path (`https://aresmcp.com/mcp`).

## 2. Authenticate (Hermes, not Claude)

```bash
hermes mcp login ares
```

Hermes will:

1. Discover Ares OAuth metadata  
2. Open a browser to aresmcp.com (Google)  
3. Complete PKCE and cache tokens under `~/.hermes/mcp-tokens/`  

Re-check:

```bash
hermes mcp test ares
# or
hermes mcp
```

You should see Ares tools listed. Re-run `hermes mcp login ares` if refresh fails.

### Headless / no browser

If the host cannot open a browser, use a token issued from the aresmcp.com account dashboard (when available) or an operator API key:

```yaml
mcp_servers:
  ares:
    url: "https://aresmcp.com/mcp"
    enabled: true
    headers:
      Authorization: "Bearer <JWT_OR_KEY>"
```

Prefer OAuth when possible — keys are broader and harder to rotate per device.

## 3. Install skills

Copy skills into Hermes:

```bash
# from a clone of this repo
cp -R hermes-plugin/skills/* ~/.hermes/skills/
```

Or symlink:

```bash
ln -s "$(pwd)/hermes-plugin/skills/ares-recon" ~/.hermes/skills/ares-recon
# …repeat for other ares-* skills
```

Restart / reload Hermes after config or skill changes (`/reload-mcp` in-session if available).

## 4. Use it

In a Hermes chat:

```text
Start an external recon engagement on example.com and produce an engagement report.
```

Typical flow the agent should follow:

1. `engagement_create`  
2. Playbook (`playbook_full_external` / `playbook_osint_person` / …)  
3. `job_status` → `engagement_summary` / `engagement_report`  

## Skills

### Surface

| Skill | Intent |
|-------|--------|
| **ares-osint** | Domain + identity OSINT |
| **ares-recon** | External attack surface |
| **ares-scan** | Web/app assessment |
| **ares-network** | Ports & services |
| **ares-cloud** | Public cloud / container exposure |
| **ares-re** | Binary / mobile triage |
| **ares-forensics** | PCAP / evidence / CTF |

### Methodology

| Skill | Intent |
|-------|--------|
| **ares-web-app** | End-to-end web + report |
| **ares-api** | API / GraphQL / auth paths |
| **ares-ad-light** | Light AD / creds |
| **ares-external-recon** | Full external one-shot |
| **ares-people-osint** | Person / email / phone / username |

Each skill sets `mcp_server: ares` so Hermes binds tool calls to this MCP server.

## MCP surface (hosted)

~200 real tools. Control plane includes:

- Discovery: `list_capabilities`, `search_tools`, `get_tool_info`, `run_tool`  
- Jobs: `job_status`, `job_cancel`, `list_jobs`, `get_findings`, `get_artifact`  
- Memory: `engagement_create`, `engagement_summary`, `engagement_assets`, `engagement_findings`, `engagement_report`, `engagement_timeline`, `engagement_suggest_next`, facts  

Pinned examples: `dns_lookup`, `subdomain_enum`, `http_probe`, `port_scan`, `nuclei_scan`, identity OSINT tools, `playbook_full_external`, `playbook_osint_*`, `playbook_api_deep`, `playbook_ad_enum`.

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Tools missing after config | `hermes mcp test ares`; ensure `enabled: true` and URL ends with `/mcp` |
| OAuth “resource mismatch” | Use Hermes build that preserves full MCP path in OAuth (path `/mcp` must stay); upgrade Hermes if on an old release |
| `hermes mcp login` says success but tool calls hang | Confirm a token file exists under `~/.hermes/mcp-tokens/`; re-login |
| 401 on every call | Re-run `hermes mcp login ares` or fix `Authorization` header |
| Long scan client timeout | Raise `timeout:` under the `ares` server entry |

## Operator posture

Ares is built for **operator-led security engagements**. The named target is the engagement scope; platform policy still blocks private/metadata/self targets. No paid third-party OSINT API keys required.

## Links

- Product: https://aresmcp.com  
- Hermes MCP docs: https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp  
- Claude Code install (separate surface): `/plugin marketplace add kareeii/ares-mcp`  
