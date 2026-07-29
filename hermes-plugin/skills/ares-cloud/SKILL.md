---
name: ares-cloud
description: Operator public-cloud and container exposure checks with Ares MCP — buckets, metadata/IMDS, Docker/K8s/etcd, image/IaC. Use for named org/domain/asset cloud exposure during a security engagement. Requires hermes mcp login ares.
category: security
mcp_server: ares
---

# Ares · Cloud

## Prerequisites

1. `ares` is configured in `~/.hermes/config.yaml` with `url: https://aresmcp.com/mcp` and `auth: oauth`.
2. Authenticate once with Hermes (not Claude Code):

```bash
hermes mcp login ares
hermes mcp test ares
```

Tokens are cached under `~/.hermes/mcp-tokens/`. There is no `/mcp` Authenticate UI in Hermes.

## Engagement posture

Named target = engagement scope for this session. Prefer `engagement_create` then playbooks; close with `engagement_report` when useful.

## Workflow

- Storage: `s3_open_check`, `bucket_enum`, `aws_takeover_check`, `azure_tenant_find`
- Control planes: `aws_imds_check`, `cloud_metadata_probe`, `docker_socket_check`, `kubernetes_api_check`, `etcd_unauth_check`
- Images/IaC: `container_scan`, `docker_image_scan`, `iac_scan`, `terraform_scan`
