---
name: re
description: Reverse engineering and binary/mobile triage with Ares (file type, strings, entropy/packing, YARA, ELF/PE analysis, disassembly, APK decompile, encoding/cipher helpers). Use proactively whenever the user has a binary, executable, firmware, or mobile (APK) sample to analyze, triage, or reverse — including CTF challenges — even if they do not mention Ares. Authorized samples only.
---

# Ares · RE

Triage and reverse-engineer an authorized binary or mobile sample.

## Scope

- Sample must be available to the job workspace (`/work/...`).
- Prefer static analysis first.

## Workflow

### 1. Composite (preferred)

```
playbook_binary_triage
```

CTF-oriented alternative: `playbook_ctf_quick`.

### 2. Static analysis

| Goal | Tools |
|------|-------|
| Identify | `file_identify`, `bin_triage` |
| Strings / packing | `strings_extract`, `entropy_analyze`, `binwalk_scan` |
| Signatures | `yara_scan` |
| ELF | `elf_protections`, `elf_analyze` |
| PE | `pe_analyze` |
| Disassembly | `objdump_disasm`, `radare2_analyze` |
| Metadata | `exiftool_meta` |

### 3. Mobile

- `jadx_decompile`
- `android_manifest`

### 4. Encoding helpers (when relevant)

- `base_decode`, `cipher_identify`, `xor_bruteforce`
- PCAP or disk-style evidence → **forensics**

### 5. Deliverable

- File type and high-level structure
- Protections and interesting strings/IOCs
- YARA hits
- Mobile components/permissions when applicable

## Rules

- Authorized samples only.
- Summarize findings; avoid pasting huge disassembly into chat.
