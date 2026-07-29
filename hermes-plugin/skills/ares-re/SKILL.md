---
name: ares-re
description: Reverse engineering and binary/mobile triage with Ares MCP (file type, strings, entropy, YARA, ELF/PE, disassembly, APK decompile, encoding helpers). Use for authorized binary/mobile sample analysis.
category: security
mcp_server: ares
---

# Ares RE

Triage and reverse-engineer an authorized binary or mobile sample.

## Prerequisites

The `ares` MCP server must be authenticated via OAuth in `/mcp` before use.
Sample must be available in the job workspace (`/work/...`).

## Scope

- Sample must be available to the job workspace.
- Prefer static analysis first.

## Workflow

### 1. Composite (preferred)

Use `playbook_binary_triage` via `run_tool`.
CTF alternative: `playbook_ctf_quick`.

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

### 4. Encoding helpers

- `base_decode`, `cipher_identify`, `xor_bruteforce`
- PCAP or disk-style evidence → forensics

### 5. Deliverable

- File type and high-level structure
- Protections and interesting strings/IOCs
- YARA hits
- Mobile components/permissions when applicable

## Rules

- Authorized samples only.
- Summarize findings; avoid pasting huge disassembly into chat.
