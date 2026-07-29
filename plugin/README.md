# Ares (Claude Code plugin)

Hosted red-team toolkit for [Claude Code](https://claude.com/claude-code).

**Also supports [Hermes Agent](../hermes-plugin/README.md)** — different install/auth path (no `/mcp` UI).

**Service:** [https://aresmcp.com](https://aresmcp.com)

## Install (Claude Code)

```text
/plugin marketplace add kareeii/ares-mcp
/plugin install ares@ares-mcp
```

## Authenticate (Claude Code)

1. Open `/mcp`
2. Select **ares** → **Authenticate** (or `claude mcp login ares`)
3. Continue with Google on aresmcp.com
4. Status becomes **connected**

Do not put Bearer tokens in plugin config.

## Skills

### Surface

| Skill | Use for |
|-------|---------|
| `osint` | Domain + identity intelligence |
| `recon` | External attack surface |
| `scan` | Web / app assessment |
| `network` | Ports and services |
| `cloud` | Public cloud / container exposure |
| `re` | Reverse engineering / binary triage |
| `forensics` | PCAP, metadata, CTF-style analysis |

### Methodology

| Skill | Use for |
|-------|---------|
| `web-app` | End-to-end web + engagement report |
| `api` | API / GraphQL / auth paths |
| `ad-light` | Light AD / creds |
| `external-recon` | Full external one-shot |
| `people-osint` | Person / email / phone / username |

## Tools

- Lean MCP surface for day-to-day work
- Full catalog via `search_tools` → `get_tool_info` → `run_tool`
- Engagement memory: `engagement_create` → … → `engagement_report`
- Async jobs: `job_status`, `get_findings`, `get_artifact`

## Hermes Agent

Hermes does **not** use `/mcp` Authenticate. See the root README and:

- [`hermes-plugin/README.md`](../hermes-plugin/README.md)
- Config: `url: https://aresmcp.com/mcp` + `auth: oauth`
- Auth: `hermes mcp login ares`

## Links

- https://aresmcp.com
- https://aresmcp.com/docs
