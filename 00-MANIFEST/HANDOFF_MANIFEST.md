# CBH MASTER HANDOFF — MANIFEST

- **Date:** 2026-11-14
- **Machine:** Kali (Linux)
- **Mode:** LOCAL ONLY (no GitHub repository created, no push executed — owner decision)
- **Phase:** DISCOVER → CLASSIFY → PRESERVE → VERIFY → HANDOFF (pre-build organization)
- **Status:** PARTIAL (local package complete; GitHub handoff NOT CREATED)

---

## 1. Classification map

| Category | What it maps to | Location in package |
|---|---|---|
| SOURCE / PRIMARY PROJECT | CBH (`bugMO77/cbh`, private) | `01-CBH/` (pointer only — no duplication) |
| REFERENCE | BUGGY, AI-HUNTING, OffsecCyber, external sources | `02-BUGGY/`, `04-AI-HUNTING/`, `05-SOURCES/` |
| METHODOLOGY | CBH Development Methodology baseline (REV2, DRAFT — OWNER REVIEW) | `03-METHODOLOGY/` |
| EVIDENCE | audit outputs, verification reports, integrity hashes, intake package | `06-EVIDENCE/` |
| GENERATED | files produced during this handoff (metadata, manifests, snapshot) | scattered; registry below |
| VALIDATION | actual execution results for CBH/V1 — NONE EXIST (NOT EXECUTED) | `07-VALIDATION/` |

## 2. Contents (48 files, ~1.28 MB)

### 00-MANIFEST/
- `HANDOFF_MANIFEST.md` (this file)
- `HANDOFF_STATUS.md`
- `HANDOFF_BLOCKED_ARTIFACTS.md`
- `SHA256SUMS.txt` (generated after all files; verifiable from package root)

### 01-CBH/
- `CBH_SOURCE_POINTER.md` — canonical repo info (remote, branch, HEAD, worktree, counts).

### 02-BUGGY/
- `buggy-git-head.txt` — original HEAD SHA, branch, remotes.
- `buggy-git-status.txt` — full `git status` at original state.
- `BUGGY_SNAPSHOT_METADATA.md` — snapshot branch/commit + ZIP hash + security matrix.
- `buggy-repo-snapshot.zip` — filesystem preservation archive (209 entries; SHA-256
  `9d04ed8f...d45e3a2`).

### 03-METHODOLOGY/
- `REV2/` — full extracted CBH Development Methodology baseline REV2 package
  (baseline md, revision notes, package manifest, SHA-256, traceability/open decisions,
  source-reference evidence files).
- `CBH-DEVELOPMENT-METHODOLOGY-BASELINE-v0.1-REV2.zip` — original package archive.

### 04-AI-HUNTING/ (metadata only — owner decision)
- `SOURCE_METADATA.md`
- `CREATOR_PERMISSION_CONTEXT.md`
- `SNAPSHOT_CURATION.md`
- `AI_HUNTING_ARCHITECTURE_REVIEW.md`
- `AI_HUNTING_COMPONENT_MAP.csv`
- Repo: `0xmannaf/Ai-Hunting` @ `3c1e9a021779eeffbd2c021b8664aa24c1df04b2` (pinned).
- Full curated snapshot is intentionally NOT included (permission not cleared).

### 05-SOURCES/ (metadata only — owner decision)
- `OFFSECCYBER_SOURCE_METADATA.md` — dataset pinned revision
  `e2aa04114f466659701cf999dfa27a2ebf7054ef`; license declared Apache-2.0;
  third-party rights UNRESOLVED; redistribution NOT CLEARED.
- `OFFSECCYBER_DATASET_REVIEW.md`
- `OFFSECCYBER_CBH_SUITABILITY.md`
- `OFFSECCYBER_SCHEMA.csv`
- `OFFSECCYBER_SAMPLE_QUALITY.csv` (inventory of sample IDs only)
- `SAMPLING_PROVENANCE.md`
- 40 sample records are intentionally NOT included (third-party rights unresolved).

### 06-EVIDENCE/
- `EVIDENCE_LIMITATIONS.md`
- `CBH_PHASE_1_3_HANDOFF.md`
- `INTAKE_PACKAGE_SHA256SUMS.txt` (integrity hashes of the reference-intake package)

### 07-VALIDATION/
- `VALIDATION_STATUS.md` — states NOT EXECUTED; no fabricated results.

## 3. Key identities

| Item | Value |
|---|---|
| CBH remote | `https://github.com/bugMO77/cbh.git` (PRIVATE) |
| CBH branch | `workspace/initial-import-2026-11-13` |
| CBH HEAD | `e2cd7a935b2a1ac8f26d845da76d8249dfeaa64d` |
| CBH worktree | CLEAN; 1185 tracked files |
| BUGGY remote | `https://github.com/bugMO77/buggy.git` (PRIVATE) |
| BUGGY original branch | `phase2/runtime-preflight-v1` |
| BUGGY original HEAD | `3ebba7b59fc9386864db260b8e1035512c5f9f6c` |
| BUGGY snapshot branch | `snapshot/kali-2026-11-14` (LOCAL ONLY) |
| BUGGY snapshot commit | `3e31816` |
| BUGGY ZIP SHA-256 | `9d04ed8f6949a90ad5cb36f65164e3f2ae1a47ee7b23ad40f64ad50b6d45e3a2` |
| Methodology status | REV2 baseline — DRAFT / OWNER REVIEW; CONFIRMED + DERIVED + PROPOSED + OPEN documented |
| AI-HUNTING | REFERENCE (metadata in package; snapshot local only) |
| OffsecCyber | REFERENCE (metadata in package; samples local only) |
| VALIDATION | NOT EXECUTED |

## 4. Blocked / missing

- BLOCKED_ARTIFACTS: see `HANDOFF_BLOCKED_ARTIFACTS.md` (reasons only).
- MISSING_ARTIFACTS:
  - `cbh-handoff` GitHub repository — NOT CREATED (owner decision: local-only now).
  - AI-HUNTING curated snapshot — intentionally omitted (metadata only).
  - OffsecCyber 40 sample records — intentionally omitted (metadata only).
  - CBH validation results — none exist.
  - BUGGY snapshot branch — created locally, NOT pushed to GitHub.

## 5. Security gate applied

- `git add -A` was NEVER used.
- Explicit staging only (24 approved files into snapshot commit).
- Secret-pattern scans run on staged content and included artifacts: no matches.
- Every included artifact classified (secrets / private / local-safe / public-safe).
- No public-unsafe artifact is inside this private local package except where expressly
  marked and required (tool-installation-report.json contains local paths).
- No uploads happen in this phase, so nothing is exposed remotely.
