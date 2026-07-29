---
name: ares-cloud
description: Public cloud and container exposure checks with Ares MCP (open buckets, metadata/IMDS, Docker/K8s/etcd, container image and IaC scanning). Use for authorized cloud security testing.
category: security
mcp_server: ares
---

# Ares Cloud

Check public cloud and container exposure for an authorized organization or asset set.

## Prerequisites

The `ares` MCP server must be authenticated via OAuth in `/mcp` before use.

## Scope

- Confirm company/domain keywords, known bucket names, or image/IaC paths.
- Avoid aggressive global name brute force.

## Workflow

### 1. Object storage and takeover signals

- `s3_open_check`, `bucket_enum`
- `azure_tenant_find`, `aws_takeover_check`

### 2. Exposed control planes (in-scope hosts only)

- `aws_imds_check`, `cloud_metadata_probe`
- `docker_socket_check`, `kubernetes_api_check`, `etcd_unauth_check`

### 3. Images and IaC (when artifacts are available)

- `container_scan`, `docker_image_scan`, `docker_history`
- `iac_scan`, `terraform_scan`

Use `get_tool_info` for exact parameters.

### 4. Deliverable

- Open or weak public storage
- Exposed admin/control endpoints
- High image/IaC findings
- Hand-off application hosts to scan or network

## Rules

- Authorized scope only.
- Prefer precise names over wide enumeration.
