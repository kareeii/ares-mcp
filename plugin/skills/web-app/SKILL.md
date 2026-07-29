---
name: web-app
description: Operator methodology for web application assessment with Ares — recon hand-off, crawl/fuzz, nuclei, headers, injection tests, engagement report. Use when the operator is assessing a web app or URL end-to-end during a security engagement.
---

# Ares · Methodology · Web App

## Goal
Structured web-app assessment with durable engagement memory and a final evidence pack.

## Workflow
1. `engagement_create` (or reuse) with `primary_target=https://app`
2. Surface: `playbook_web_recon` / `http_probe` / `web_crawl` / `dir_fuzz`
3. Triage: `playbook_vuln_triage` or `nuclei_scan` (uses memory URLs when stateful)
4. Auth/config: `security_headers`, `cors_test`, `oauth_misconfig`
5. Injection when relevant: `sqli_test`, `xss_test`, `lfi_test`, `ssrf_test`
6. Close: `engagement_report` + `engagement_suggest_next`

## Deliverable
`engagement_report` executive summary, high findings, paths, timeline.
