---
name: cloud
description: Operator public-cloud and container exposure checks with Ares — open buckets, cloud metadata/IMDS, exposed Docker/Kubernetes/etcd, container image and IaC scanning. Use whenever the operator is reviewing cloud, S3/bucket, container, Kubernetes, or IaC/Terraform exposure for a named org or asset during a security engagement — even if they do not say "Ares".
---

# Ares · Cloud

Public cloud and container exposure checks for an operator-led engagement.

## Engagement posture

Named org/domain/bucket/image = engagement scope. Proceed with checks; pair with **recon** / **osint** when the seed is only a domain or org name. Avoid aimless global name brute force.

### 0. Engagement memory

```
engagement_create
  name: cloud <org-or-domain>
  primary_target: <domain|org>
```

Pull candidates from `engagement_assets` when recon already ran.

### 1. Object storage and takeover signals

- `s3_open_check`, `bucket_enum`
- `azure_tenant_find`, `aws_takeover_check`

### 2. Exposed control planes (engagement hosts only)

- `aws_imds_check`, `cloud_metadata_probe`
- `docker_socket_check`, `kubernetes_api_check`, `etcd_unauth_check`

### 3. Images and IaC (when artifacts are available)

- `container_scan`, `docker_image_scan`, `docker_history`
- `iac_scan`, `terraform_scan`

### 4. Deliverable

Open/weak public storage, exposed admin endpoints, high image/IaC findings. Hand off app hosts to **scan** or **network**.
