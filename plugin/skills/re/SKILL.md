---
name: re
description: Operator reverse-engineering and binary/mobile triage with Ares — file type, strings, entropy/packing, YARA, ELF/PE, disassembly, APK decompile, encoding/cipher helpers. Use whenever the operator is triaging or reversing a binary, executable, firmware, or mobile (APK) sample during an engagement or CTF — even if they do not say "Ares".
---

# Ares · RE

Static-first triage for binaries and mobile samples in an operator workspace.

## Engagement posture

Sample in the job workspace is the engagement artifact. Prefer static analysis first. Strings/metadata often expose URLs, IPs, emails, keys — record via engagement facts and pivot to **osint** / **network** / **cloud**.

### 0. Engagement (optional)

```
engagement_create
  name: re <sample>
  primary_target: <sample-or-family-name>
```

### 1. Composite

`playbook_binary_triage` · CTF path `playbook_ctf_quick`

### 2. Static analysis

`file_identify` / `bin_triage` · strings / entropy / binwalk · YARA · ELF/PE · objdump / radare2 · `exiftool_meta`

### 3. Mobile

`jadx_decompile` · `android_manifest`
