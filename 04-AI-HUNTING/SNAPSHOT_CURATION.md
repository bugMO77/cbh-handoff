# SNAPSHOT_CURATION.md — Ai-Hunting source snapshot

**Repository:** https://github.com/0xmannaf/Ai-Hunting
**Commit:** `3c1e9a021779eeffbd2c021b8664aa24c1df04b2`
**Commit date (verified locally):** 2026-10-06T18:42:40+03:00
**Snapshot path:** `external-sources/ai-hunting/source-snapshot/`
**Curation date:** 2026-11-04

---

## 1. Method

- Fresh `git clone` of the public repository.
- `git rev-parse HEAD` = `3c1e9a021779eeffbd2c021b8664aa24c1df04b2` (matches the inspected commit).
- `git checkout 3c1e9a0...` (already at pinned commit).
- Curated copy created into `source-snapshot/` preserving original repository paths.
- `.git/` excluded.
- Original working clone retained **outside** the package at
  `/tmp/opencode/ai-hunting-working-copy/` for reference; it is **not** included in the ZIP.

## 2. Counts

| Item | Count |
|------|------:|
| Files tracked by git at pinned commit | 312 |
| Included in curated snapshot | 154 |
| Excluded: `testing/` | 157 |
| Excluded: `scripts/__probe__/` | 1 |

`312 − 157 − 1 = 154` (consistent).

## 3. Exclusions and rationale

### 3.1 `.git/` — excluded
Internal version-control metadata (objects, refs, hooks). Not needed for architecture
study, and can contain credentials in some clones. Not part of the source content.

### 3.2 `testing/` — excluded (157 files)
This directory contains **real target-specific evidence** collected against live or
public targets:

- raw HTTP responses (`responses/*.html`, `*.txt`, `*.json`)
- scan outputs (`scans/*`)
- session/credential-adjacent scripts (`scripts/forge_session.py`, `verify_passwords.py`)
- a database dump (`responses/db_dump.txt`)
- dorking notes that matched a strict credential pattern
  (`notes/dorking.md` — credential-like string detected; values not reproduced here)

Rationale for exclusion:

- Explicit instruction to exclude secrets, tokens, cookies, authentication headers, private
  user data, and sensitive target-specific request/response evidence.
- These artefacts do **not** contribute to understanding the architecture, and several are
  unrelated to the project's reusable design.
- They carry privacy and third-party risk if redistributed, even privately.

**Note:** these files are still part of the public repository; they were simply not copied
into this package. The full working clone remains outside the ZIP.

### 3.3 `scripts/__probe__/learning_engine/memory/learning.db` — excluded (1 file)
A binary SQLite probe database (114,688 bytes) under `scripts/__probe__/`. It is a runtime
probe artefact of uncertain content, not source or documentation needed to understand the
architecture. Excluded rather than exposed.

### 3.4 Secret scan performed
A strict credential-pattern scan (`AKIA…`, `ghp_…`, `xox[baprs]-…`, `sk-…`, private-key
blocks) was run over the working clone. Matches were found **only** within the excluded
`testing/` tree. No credential values are reproduced in this package.

## 4. Included content (categories)

- Root documentation: `AGENTS.md`, `agent-briefing.md`, `prioritization.md`, `prompts.md`
- Agent/command definitions: `runtime/`, `.opencode/`, `.opencode.json`, `opencode.json`
- Skills: `skills/` and `.agents/skills/` (22 skill playbooks each)
- Learning engine: `learning_engine/`
- Memory templates: `memory/`
- Runtime scripts: `scripts/` (excluding `__probe__/`)
- References and config: `references/`, `package.json`, `.gitignore`
- CI configuration: `.github/workflows/`
- Sample/illustrative writeups: `writeups/` (sample feeds included in the repository)
- Wordlist README: `wordlist/`

## 5. Integrity note

Because `.git` is excluded, the snapshot cannot be hash-verified against git objects inside
the package. It is verified by:

- the pinned commit SHA recorded here and in `SOURCE_METADATA.md`;
- per-file SHA-256 checksums in `integrity/SHA256SUMS.txt`;
- the reproducible curation method above (re-clone at pinned commit + exclusions).
