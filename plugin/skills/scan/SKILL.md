---
name: scan
description: Web vulnerability assessment with Ares — crawl, directory fuzz, nuclei, headers, gated injection tests.
---

# Ares · Scan

Assess an authorized web application for vulnerabilities.

## Scope

- Confirm the exact origin (scheme + host).
- Agree whether intrusive injection tests are allowed.
- Default to critical/high, non-destructive checks first.

## Workflow

### 1. Composite (preferred)

```
playbook_web_app_test
```

or

```
playbook_vuln_triage
  target: https://<host>
```

Then `job_status` → `get_findings(severity_min="medium")`.

### 2. Discovery

| Goal | Tools |
|------|-------|
| Landing / headers | `fetch_url`, `security_headers`, `cookie_security`, `hsts_check` |
| Crawl / JS | `web_crawl`, `js_endpoint_extract`, `js_secrets_scan` |
| Content discovery | `dir_fuzz`, `param_mine`, `param_fuzz`, `backup_file_scan`, `git_exposure` |
| API | `api_probe`, `graphql_probe`, `swagger_scan` |
| CMS | `cms_scan`, `wordpress_users` |

### 3. Scanners

- `nuclei_scan` — start with `profile=critical_high`
- `nuclei_dast` / `nikto_scan` when useful
- Light checks: `cors_test`, `clickjacking_test`, `ssl_audit`, `waf_detect`, `oauth_misconfig`

### 4. Intrusive tests (explicit approval required)

Pass `confirm: true` only after the user authorizes:

- `sqli_test`, `xss_test`, `lfi_test`, `ssrf_test`
- Related: `crlf_test`, `host_header_inject`, `open_redirect_test`

### 5. Deliverable

1. Critical / high findings with evidence  
2. Medium misconfigurations  
3. Notable paths/tech (info)  
4. Suggested retest commands  

## Rules

- Authorized targets only.
- Intrusive tools require user approval and `confirm=true`.
- Prefer filtered `get_findings` over raw scanner dumps.
