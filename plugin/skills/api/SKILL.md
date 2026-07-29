---
name: api
description: Operator methodology for API security assessment with Ares — endpoint discovery, GraphQL/Swagger, auth path checks, JWT inspection. Use when the operator is testing an API or GraphQL endpoint during a security engagement.
---

# Ares · Methodology · API

## Workflow
1. `engagement_create` with API base URL
2. `playbook_api_deep` (crawl/JS → api/graphql/swagger → `api_auth_check`)
3. `jwt_none_check` when tokens appear
4. `graphql_probe` / `swagger_scan` deepen as needed
5. `engagement_report`

## Notes
Prefer engagement memory for discovered endpoints; no paid API scanners.
