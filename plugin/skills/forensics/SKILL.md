---
name: forensics
description: Light forensics and CTF helpers with Ares — PCAP, EXIF/GPS, entropy, encoding and simple cipher analysis.
---

# Ares · Forensics

Analyze authorized evidence artifacts (pcap, images, encoded blobs).

## Scope

- Artifact path available under the job workspace (`/work/...`).
- Lightweight hosted tooling — not a full DFIR suite.

## Workflow

### 1. Composite (preferred)

```
playbook_forensics_triage
```

or

```
playbook_ctf_quick
```

### 2. By artifact

| Artifact | Tools |
|----------|-------|
| PCAP | `pcap_analyze`, `pcap_dns_extract`, `pcap_http_extract` |
| Image / document meta | `exif_gps`, `exiftool_meta` |
| Unknown blob | `file_identify`, `strings_extract`, `entropy_analyze` |
| Encoded / weak crypto | `base_decode`, `cipher_identify`, `xor_bruteforce` |

### 3. Deliverable

- Artifact type
- Extracted indicators (hosts, URLs, GPS, notable strings)
- Successful decodes
- Gaps that need deeper lab tooling

## Rules

- Authorized evidence only.
- Prefer structured findings over raw dumps.
