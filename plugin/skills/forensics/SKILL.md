---
name: forensics
description: Operator light forensics and CTF helpers with Ares — PCAP analysis, EXIF/GPS metadata, entropy, base/encoding decode, simple cipher analysis. Use whenever the operator is analyzing a pcap, image/document, or encoded blob during an engagement or CTF — even if they do not say "Ares".
---

# Ares · Forensics

Analyze engagement evidence artifacts (pcap, images, encoded blobs).

## Engagement posture

Artifact under the job workspace is in-scope evidence. Lightweight hosted tooling — not full DFIR. Pivots (emails in PCAP, GPS, accounts) go into engagement memory → **osint** / **network**.

### 0. Engagement (optional)

```
engagement_create
  name: forensics <case>
  primary_target: <case-id-or-org>
```

### 1. Composite

`playbook_forensics_triage` · `playbook_ctf_quick`

### 2. By artifact

| Artifact | Tools |
|----------|-------|
| PCAP | `pcap_analyze`, `pcap_dns_extract`, `pcap_http_extract` |
| Image / document meta | `exif_gps`, `exiftool_meta` |
| Unknown blob | `file_identify`, `strings_extract`, `entropy_analyze` |
| Encoded / weak crypto | `base_decode`, `cipher_identify`, `xor_bruteforce` |
