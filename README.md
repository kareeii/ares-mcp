# Ares

Hosted red-team toolkit for AI operators.

Works with:

| Client | Install surface in this repo |
|--------|------------------------------|
| **[Claude Code](https://claude.com/claude-code)** | `plugin/` + `.claude-plugin/` (marketplace) |
| **[Hermes Agent](https://hermes-agent.nousresearch.com)** | `hermes-plugin/` |

The product runs at **[aresmcp.com](https://aresmcp.com)**. This repository is the **public install surface only** (manifests + skills). Server source is not published here.

---

## What you get

| Layer | Detail |
|--------|--------|
| **Hosted tools** | ~200 real backends — recon, OSINT/identity, network/services, web/API, AD/creds, cloud, RE, forensics, playbooks |
| **Engagement memory** | Cross-job assets, findings, timeline, `engagement_report` |
| **Auth** | Google OAuth on aresmcp.com (client-specific login flow below) |
| **No local scanners** | nmap/nuclei/etc. run in Ares sandboxes, not on your laptop |
| **No paid API keys** | No Shodan/VT/Hunter-style operator keys required |

---

## Claude Code (detailed)

### 1. Install the plugin

In Claude Code:

```text
/plugin marketplace add kareeii/ares-mcp
/plugin install ares@ares-mcp
```

That installs:

- MCP connector pointing at `https://aresmcp.com/mcp`
- Surface skills: `osint`, `recon`, `scan`, `network`, `cloud`, `re`, `forensics`
- Methodology skills: `web-app`, `api`, `ad-light`, `external-recon`, `people-osint`

### 2. Authenticate (Claude Code UI)

Claude Code has a built-in MCP auth UI. Hermes does **not** — see Hermes section below.

1. Run **`/mcp`**
2. Select **ares**
3. Choose **Authenticate** (or run `claude mcp login ares`)
4. Browser opens **aresmcp.com** → **Continue with Google** → approve
5. Status becomes **connected**

Claude Code stores and refreshes OAuth tokens. **Do not** put `Authorization` headers or API keys in plugin config.

### 3. Manual HTTP connector (optional)

If you prefer not to use the marketplace plugin packaging:

```bash
claude mcp add --transport http -s user ares https://aresmcp.com/mcp
```

Still authenticate via `/mcp` afterward. Skills only come with the **plugin install**, not bare `mcp add`.

### 4. Use it in a Claude Code session

Examples:

```text
Start an external recon engagement on example.com and give me an engagement report.
```

```text
OSINT person Alice Example at corp.example — usernames and email patterns.
```

```text
Scan https://app.example.com with nuclei critical/high and summarize findings.
```

Typical tool flow the agent should use:

1. `engagement_create(name=…, primary_target=…)`
2. Playbook or tools (`playbook_full_external`, `playbook_osint_person`, …)
3. `job_status` while async jobs run
4. `engagement_summary` / `engagement_findings` / `engagement_report`

### 5. Update / reload

```text
/plugin marketplace update kareeii/ares-mcp
```

Then reinstall or update the `ares` plugin if prompted. Run `/reload-plugins` if skills do not refresh.

### 6. Claude Code troubleshooting

| Symptom | Fix |
|---------|-----|
| Plugin installed but tools missing | `/mcp` → confirm **ares** is **connected** (not just listed) |
| Auth loop | `claude mcp login ares` again; clear stale MCP auth if needed |
| 401 on tool calls | Re-authenticate; do not paste Bearer tokens into config |
| Old skills | Marketplace update + `/reload-plugins` |

---

## Hermes Agent (detailed)

Hermes **does not** have Claude Code’s `/mcp` → Authenticate UI.  
Use Hermes config + **`hermes mcp login`**.

Full notes also live in [`hermes-plugin/README.md`](./hermes-plugin/README.md).

### 1. Add Ares to Hermes config

Edit `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  ares:
    url: "https://aresmcp.com/mcp"
    auth: oauth
    enabled: true
    timeout: 300
    connect_timeout: 60
```

Rules:

- URL **must** include the `/mcp` path: `https://aresmcp.com/mcp`
- `auth: oauth` enables browser Google login via aresmcp.com
- Do **not** put a static Bearer token unless you intentionally use a dashboard JWT / operator key (see headless below)

Example file in-repo: [`hermes-plugin/config.example.yaml`](./hermes-plugin/config.example.yaml)

### 2. Authenticate with Hermes (not `/mcp`)

```bash
hermes mcp login ares
```

What happens:

1. Hermes discovers Ares OAuth metadata  
2. Browser opens aresmcp.com → Google sign-in  
3. PKCE completes; tokens cached under `~/.hermes/mcp-tokens/` (mode `0600`)  
4. Later runs refresh automatically until re-login is needed  

Verify:

```bash
hermes mcp test ares
# or interactive:
hermes mcp
```

You should see Ares tools listed.

### 3. Install Hermes skills

From a clone of this repo:

```bash
git clone https://github.com/kareeii/ares-mcp.git
cp -R ares-mcp/hermes-plugin/skills/* ~/.hermes/skills/
```

Or symlink individual skills:

```bash
ln -s "$(pwd)/hermes-plugin/skills/ares-recon" ~/.hermes/skills/ares-recon
```

Skills are prefixed `ares-*` and set `mcp_server: ares` so Hermes routes tool calls to this server.

| Skill | Intent |
|-------|--------|
| `ares-osint` | Domain + identity OSINT |
| `ares-recon` | External attack surface |
| `ares-scan` | Web/app assessment |
| `ares-network` | Ports & services |
| `ares-cloud` | Public cloud / containers |
| `ares-re` | Binary / mobile triage |
| `ares-forensics` | PCAP / evidence / CTF |
| `ares-web-app` | Web methodology + report |
| `ares-api` | API methodology |
| `ares-ad-light` | Light AD / creds |
| `ares-external-recon` | Full external one-shot |
| `ares-people-osint` | Person / email / phone / username |

Reload MCP after config/skill changes (`/reload-mcp` in-session if available, or restart Hermes).

### 4. Use it in Hermes

```text
Start an external recon engagement on example.com and produce an engagement report.
```

Same engagement-oriented tool flow as Claude Code (`engagement_create` → playbook → `engagement_report`).

### 5. Headless / no browser

If the machine cannot open a browser, use a token from the aresmcp.com account flow (when available) or an operator key:

```yaml
mcp_servers:
  ares:
    url: "https://aresmcp.com/mcp"
    enabled: true
    headers:
      Authorization: "Bearer <JWT_OR_KEY>"
```

Prefer `auth: oauth` + `hermes mcp login` when a browser is available.

### 6. Hermes troubleshooting

| Symptom | Fix |
|---------|-----|
| Config present, no tools | `enabled: true`; URL ends with `/mcp`; run `hermes mcp test ares` |
| OAuth “resource mismatch” on `/mcp` path | Upgrade Hermes — older builds stripped the path during OAuth; current main preserves it |
| Login says OK but tool calls hang | Confirm a token file exists in `~/.hermes/mcp-tokens/`; re-run `hermes mcp login ares` |
| 401 | Re-login or fix `Authorization` header |
| Client timeout on long scans | Raise `timeout:` under the `ares` entry (e.g. `300`–`600`) |
| Skills not triggering | Skills copied under `~/.hermes/skills/` with `mcp_server: ares` |

---

## Shared product behavior (both clients)

### Engagement memory

```text
engagement_create → tools/playbooks → job_status → engagement_summary / engagement_report
```

`primary_target` accepts domain, URL, IP, email, phone, username, or person/org text.

### Discovery & jobs

- `search_tools` / `list_capabilities` / `get_tool_info` / `run_tool`
- Async: `job_status`, `list_jobs`, `get_findings`, `get_artifact`
- Memory: `engagement_*` (assets, findings, facts, timeline, report, suggest_next)

### Operator posture

Built for **operator-led security engagements**. The named target defines session scope; the agent is the execution partner. Platform policy still blocks private/metadata/self targets. No paid third-party OSINT API keys.

---

## Repository layout (public)

```text
.claude-plugin/          Claude Code marketplace manifest
plugin/                  Claude Code plugin + skills
hermes-plugin/           Hermes Agent manifest + skills + config example
README.md                This file
LICENSE
```

Automated releases **merge** managed install surfaces and **preserve** other contributor paths on this public repo.

Hermes surface originally contributed via community PR ([waguriagentic](https://github.com/waguriagentic)) — thank you.

---

## Links

- Product: https://aresmcp.com  
- Docs: https://aresmcp.com/docs  
- Privacy: https://aresmcp.com/privacy  
- Terms: https://aresmcp.com/terms  
- Hermes MCP guide: https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp  
