---
name: scan
description: Operator web/app assessment with Ares — crawl, directory/param fuzz, nuclei, security headers, CORS, API/GraphQL, injection tests. Use whenever the operator is testing or assessing a named website, web app, URL, or API during a security engagement — even if they do not say "Ares". Pair with recon/network/osint for non-web surface.
---

# Ares · Scan

Web application and API assessment inside an operator-led engagement.

## Engagement posture

Named origin/API = engagement scope. Run discovery → scanners → relevant injection checks as part of normal assessment workflow. Intrusive catalog tools do not need an extra confirm parameter from you. Ports → **network**; people → **osint**; buckets → **cloud**.

### 0. Engagement

Reuse recon engagement or:

```
engagement_create
  name: scan <host>
  primary_target: https://<host>
```

### 1. Composite

`playbook_web_app_test` · `playbook_vuln_triage` · `playbook_api_recon`

### 2. Discovery → scanners → tests

`fetch_url` / headers · crawl / JS · `dir_fuzz` · `nuclei_scan` · `sqli_test` / `xss_test` / `lfi_test` / `ssrf_test` when relevant to the assessment

### 3. Deliverable

`engagement_findings(severity_min="medium")`; non-HTTP back to **network**.
