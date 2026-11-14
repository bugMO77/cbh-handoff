# CBH Phase 1–3 Audit Handoff

**Repository:** `/home/kali/cbh-dev`
**Baseline commit:** `9269278fec34d7d75bdf682a3d9b26c98339d648`
**Inspection dates:** 2026-11-03 (Phase 2 completion)
**This document date:** 2026-11-04
**CBH audit source:** `/tmp/opencode/cbh-audit/`

> **QA correction notice (2026-11-04).** Several counts in the earlier draft of this
> handoff were wrong. Corrected figures are used throughout:
> `_evidence/` contains **93** files (not 33); `TARGETED_INSPECTED` rows = **167**
> (not 265); `FULL_READ` rows = **26** (not 33); Phase 2 contains **17** files including
> **12** batch documents (11 numbered batches + `batch02-original.md`). Evidence is listed
> individually in `inventories/CBH_SOURCE_INVENTORY.csv`.

---

## 1. Phase status summary

| Phase | Description | Status | Evidence source |
|-------|-------------|--------|-----------------|
| Phase 1 | Repository & architecture baseline | COMPLETE | `all_files.txt` (310 lines), `tracked.txt` (298 lines) |
| Phase 2 | Skills deep audit (83 SKILL.md) | COMPLETE | `skills-deep/` — 4 reports + `remaining_manifest.json` + 12 batch files |
| Phase 3 | Project-wide value assessment (298 files) | COMPLETE | `project-value-assessment/` — 4 reports + `_evidence/` (93 files) |

---

## 2. Audit coverage

### Phase 1 coverage

- **File listing:** 310 entries (`all_files.txt`, includes untracked/ignored files)
- **Git-tracked files:** 298 entries (`tracked.txt`)
- **Method:** file listing and architecture overview via persisted read payloads.
- **Original artifacts in the package:** `all_files.txt`, `tracked.txt`.
  `phase-1/README.md` is **GENERATED** by the package preparation, not part of the original
  audit output.

### Phase 2 coverage (skills deep audit)

- **Skill directories:** 83
- **SKILL.md documents:** 83 (100% `FULL_VERBATIM_READ`)
- **Supporting files:** 22 (15 references, 3 scripts, 2 assets, 2 READMEs)
- **Total files under `skills/`:** 105
- **Total SKILL.md bytes:** 1,678,896
- **Method:** all 83 SKILL.md files read verbatim end-to-end; 22 supporting files inspected
  through a delegated agent.
- **Artifacts in the package:** 17 files —
  - 4 reports: `SKILLS_INVENTORY.md`, `SKILLS_CAPABILITY_MATRIX.md`,
    `SKILLS_DEEP_FINDINGS.md`, `SKILLS_AUDIT_COVERAGE.md`
  - `remaining_manifest.json`
  - 12 batch documents under `batches/`: `batch01.md` … `batch11.md` plus
    `batch02-original.md`

### Phase 3 coverage (project-wide assessment)

- **Files assessed:** 298
- **`evidence_reference` distribution (sums to 298):**

  | Reference | Rows |
  |-----------|-----:|
  | `TARGETED_INSPECTED (Phase 3)` | 167 |
  | `FULL_READ (Phase 1/2 persisted payloads)` | 26 |
  | `FULL_VERBATIM_READ (Phase 2 deep audit)` | 83 |
  | `INSPECTED (Phase 2 supporting-file review)` | 22 |
  | **Total** | **298** |

- **Evidence files saved:** **93** under `project-value-assessment/_evidence/`
  (52 `skills__*`, 15 `commands__*`, 9 `engine__*`, 6 `scripts__*`, 4 `docs__*`,
  3 `eval__*`, 2 `research__*`, 1 `cbh__*`, plus `file_meta.txt`).
- **Method:** targeted static inspection; no reads of the 83 skills were repeated; Phase 1
  and Phase 2 evidence was reused.

---

## 3. Verification of copied artifacts against originals

All three phases were compared byte-for-byte against `/tmp/opencode/cbh-audit/` with
`diff -rq`:

| Packaged path | Original path | Result |
|---------------|---------------|--------|
| `source-artifacts/cbh/phase-1/all_files.txt` | `cbh-audit/all_files.txt` | identical |
| `source-artifacts/cbh/phase-1/tracked.txt` | `cbh-audit/tracked.txt` | identical |
| `source-artifacts/cbh/phase-2/skills-deep/` | `cbh-audit/skills-deep/` | identical (17 files) |
| `source-artifacts/cbh/phase-3/project-value-assessment/` | `cbh-audit/project-value-assessment/` | identical (97 files) |

Originals were **not modified**. `phase-1/README.md` has no original counterpart and is
marked GENERATED in the inventory.

---

## 4. Phase 2 supporting files — omission record

The 22 supporting files were read during the original Phase 2 audit, but **their raw content
was never placed in `/tmp/opencode/cbh-audit/`** and is therefore **not present in this
package**. They remain part of the CBH repository at the baseline commit.

Preserved originals (paths relative to the CBH repository root):

| # | Path |
|---|------|
| 1 | `skills/offensive-osint/README.md` |
| 2 | `skills/offensive-osint/references/breach-and-credentials.md` |
| 3 | `skills/offensive-osint/references/dork-corpus.md` |
| 4 | `skills/offensive-osint/references/helpers-and-automation.md` |
| 5 | `skills/offensive-osint/references/identity-fabric.md` |
| 6 | `skills/offensive-osint/references/people-osint.md` |
| 7 | `skills/offensive-osint/references/probes-and-wordlists.md` |
| 8 | `skills/offensive-osint/references/recon-stack.md` |
| 9 | `skills/offensive-osint/references/recon-techniques.md` |
| 10 | `skills/offensive-osint/references/saas-public-surfaces.md` |
| 11 | `skills/offensive-osint/references/secret-patterns.md` |
| 12 | `skills/offensive-osint/references/secret-validators.md` |
| 13 | `skills/offensive-osint/references/sector-notes.md` |
| 14 | `skills/offensive-osint/references/severity-matrix.md` |
| 15 | `skills/offensive-osint/references/specialized-osint.md` |
| 16 | `skills/offensive-osint/references/tooling-install.md` |
| 17 | `skills/offensive-osint/scripts/assets/FONT-LICENSE.txt` |
| 18 | `skills/offensive-osint/scripts/assets/archivo-black.woff2` |
| 19 | `skills/offensive-osint/scripts/dashboard.py` |
| 20 | `skills/offensive-osint/scripts/h1_reference.py` |
| 21 | `skills/offensive-osint/scripts/secret_scan.py` |
| 22 | `skills/osint-methodology/README.md` |

Their inspection results are summarised per file in
`skills-deep/SKILLS_AUDIT_COVERAGE.md` §"Supporting files (22)" and
`skills-deep/SKILLS_INVENTORY.md` §"Supporting files (22)". The delegated-agent read payload
was stored outside `cbh-audit` and is **not reproduced here**; it is recorded as an external
reference only.

Status in the package inventory: **NOT_COLLECTED (summary evidence only)**.

---

## 5. Main findings (from the original Phase 2 and Phase 3 reports)

### 5.1 Phase 2 key findings (skills layer)

1. **Corpus structure:** 58 `hunt-*` attack-class skills + 25 non-hunt workflow skills
   (recon, OSINT, reporting, validation, enterprise).
2. **Engine integration:**
   - `engine/skill_map.py` maps 57/58 `hunt-*` skills.
   - `hunt-dispatch` is command-loaded (not mapper-driven).
   - 0 of 25 non-hunt skills are referenced by the mapper.
   - The engine defaults to `skills_on=False`.
3. **Quality defects found:**
   - 1 raw NUL byte in `skills/hunt-auth-bypass/SKILL.md` (byte offset 23277).
   - Generic template descriptions on hub skills (`hunt-rce`, `hunt-misc`, `hunt-idor`,
     `hunt-oauth`).
   - 11 skills exceed the 500-line body guideline.
   - 3 descriptions exceed the 1024-character limit (grandfathered).
   - Stale cross-references: `hunt-cache-poisoning` → `hunt-cache-poison`,
     `hunt-subdomain-takeover` → `hunt-subdomain`.
4. **Safety findings (S1–S10):**
   - Redis `flushall` / `CONFIG SET` webshell instructions (`hunt-nosqli`).
   - Admin delete used as JWT proof (`hunt-jwt-crypto`).
   - `/actuator/shutdown` treated as a finding (`hunt-springboot`).
   - Firebase write test and bucket brute force (`hunt-cloud-misconfig`).
   - 1,000,000-request OTP brute force (`hunt-mfa-bypass`).
   - Unchecked exploit downloads (`hunt-deserialization`).
   - Smuggling against a shared CDN (`hunt-http-smuggling`).
5. **Missing capabilities:**
   - Wireless / RF / physical red team.
   - Internal AD attack paths (BloodHound / Impacket / Certipy).
   - Social engineering / phishing infrastructure.
   - HTTP/3, QUIC, WebRTC.
   - Container escape / runtime Kubernetes exploitation.
   - Formal scope / rules-of-engagement template.

### 5.2 Phase 3 key findings (project-wide)

1. **CLI vs engine overlap:** both `cbh/cli.py` and `engine/engine.py` implement recon and
   surface mapping — unresolved architectural concern.
2. **Agent provider coupling:** `engine/agent.py` hard-codes the `claude` CLI; skills are
   disabled by default.
3. **Disposition summary:**
   - 267 KEEP AS-IS
   - 18 MODIFY
   - 12 OPTIONAL
   - 1 DEPRECATE (`scripts/cbh.py` shim)
   - 0 REFACTOR (deferred to Phase 4)
   - 0 MERGE (deferred to Phase 4)
4. **Dependency graph:** 90 relationships documented; no circular dependencies observed.
5. **Evidence/validation:** the eval layer provides honest evidence including the Juice Shop
   ceiling-effect caveat; the runtime verification gap is documented.

---

## 6. Important architectural observations

1. **Two-product skill layer:**
   - Engine arsenal: 58 `hunt-*` skills (57 mapper-selected + 1 command-loaded).
   - Harness-native knowledge base: 83 skills auto-activated by the host agent.
2. **Skills disabled by default:** `engine/agent.py` defaults to `skills_on=False`; the engine
   injects skill names and starter probes, not bodies.
3. **Scope enforcement is post-hoc:** `cbh/cli.py` does not enforce scope at the CLI level;
   the engine flags out-of-scope hosts only after a candidate is produced.
4. **Report references:** 70 `reports/NNN` references point to a non-existent `reports/`
   tree; they are likely HackerOne IDs requiring `H1 #NNN` notation.
5. **Evaluation limitation:** full agent evals require Docker + Burp + an authenticated
   `claude` CLI and are not reproducible on hosted CI.

---

## 7. Known limitations of the assessments

1. **Phase 2 limitations:**
   - All 83 skills read verbatim, but no runtime execution was performed.
   - Tool names inside code blocks indicate documentary commands, not verified installations.
   - "MCP named" ≠ "MCP tool contract" — only 2 skills name concrete Burp MCP tools.
   - Browser-required skills (clickjacking, CORS, DOM XSS) have no supported engine execution
     path.
   - The 22 supporting files are not reproduced in this package (see §4).
2. **Phase 3 limitations:**
   - 298 files assessed, not equally inspected — targeted inspection model.
   - 93 evidence files captured; the remaining files were targeted-inspected.
   - Runtime verification gaps are documented in `PROJECT_VALUE_ASSESSMENT.md` §7.
   - MERGE and REFACTOR were not independently resolved — deferred to Phase 4.
3. **KEEP AS-IS caveat:**
   - Does not mean perfect or immune to future architectural change.
   - Does not mean runtime behaviour was verified.
   - Does not mean safety issues are resolved.

---

## 8. Missing or incomplete evidence

| Item | Status | Notes |
|------|--------|-------|
| Phase 1 detailed architecture report | NOT SEPARATELY PRESENT | Baseline listings + Phase 1 payloads used |
| Phase 2 batch files | PRESENT | 12 files (`batch01`–`batch11` + `batch02-original`) |
| Phase 2 22 supporting files (raw) | NOT COLLECTED | Summary evidence only; paths in §4 |
| Phase 3 `_evidence/` | PRESENT | 93 files (earlier "33" was wrong) |
| `engine/burp-mcp.json` | ABSENT (only `.example` tracked) | Breaks `--strict-mcp-config` runs |
| Template for `redteam-report-template` | ABSENT | `templates/reference.docx` not shipped |
| `reports/NNN` path resolution | UNCLEAR | Likely H1 IDs, not repo paths |

---

## 9. Phase 3 classification detail

**Verified from the original CSV files:**

- 298 files assessed (`PROJECT_FILE_INVENTORY.csv`, 298 rows)
- 267 KEEP AS-IS
- 18 MODIFY
- 12 OPTIONAL
- 1 DEPRECATE
- 90 dependency relationships (`DEPENDENCY_IMPACT_MATRIX.csv`, 90 rows)
- 298/298 rows have `assessment_status = ASSESSED`
- 93 targeted-inspection evidence files saved
- MERGE and REFACTOR not independently resolved
- KEEP AS-IS does not mean perfect or immune to future architectural change

---

## 10. References to original supporting files

### Phase 1 artifacts

```
/tmp/opencode/cbh-audit/all_files.txt      — complete file listing (310 lines)
/tmp/opencode/cbh-audit/tracked.txt        — git-tracked files (298 lines)
```

### Phase 2 artifacts (skills deep audit)

```
/tmp/opencode/cbh-audit/skills-deep/SKILLS_INVENTORY.md
/tmp/opencode/cbh-audit/skills-deep/SKILLS_CAPABILITY_MATRIX.md
/tmp/opencode/cbh-audit/skills-deep/SKILLS_DEEP_FINDINGS.md
/tmp/opencode/cbh-audit/skills-deep/SKILLS_AUDIT_COVERAGE.md
/tmp/opencode/cbh-audit/skills-deep/remaining_manifest.json
/tmp/opencode/cbh-audit/skills-deep/batches/batch01.md … batch11.md
/tmp/opencode/cbh-audit/skills-deep/batches/batch02-original.md
```

### Phase 3 artifacts (project-wide value assessment)

```
/tmp/opencode/cbh-audit/project-value-assessment/PROJECT_VALUE_ASSESSMENT.md
/tmp/opencode/cbh-audit/project-value-assessment/PROJECT_FILE_INVENTORY.csv
/tmp/opencode/cbh-audit/project-value-assessment/DEPENDENCY_IMPACT_MATRIX.csv
/tmp/opencode/cbh-audit/project-value-assessment/PROJECT_DECISION_MATRIX.csv
/tmp/opencode/cbh-audit/project-value-assessment/_evidence/   (93 files, listed individually in inventories/CBH_SOURCE_INVENTORY.csv)
```

---

## 11. Collected source-file preservation

```
/tmp/opencode/cbh-reference-intake/source-artifacts/cbh/
├── phase-1/
│   ├── all_files.txt          ORIGINAL  (310 lines)
│   ├── tracked.txt            ORIGINAL  (298 lines)
│   └── README.md              GENERATED by package preparation
├── phase-2/
│   └── skills-deep/           ORIGINAL  (17 files)
│       ├── SKILLS_INVENTORY.md
│       ├── SKILLS_CAPABILITY_MATRIX.md
│       ├── SKILLS_DEEP_FINDINGS.md
│       ├── SKILLS_AUDIT_COVERAGE.md
│       ├── remaining_manifest.json
│       └── batches/           (batch01–batch11 + batch02-original = 12 files)
└── phase-3/
    └── project-value-assessment/   ORIGINAL (97 files)
        ├── PROJECT_VALUE_ASSESSMENT.md
        ├── PROJECT_FILE_INVENTORY.csv
        ├── DEPENDENCY_IMPACT_MATRIX.csv
        ├── PROJECT_DECISION_MATRIX.csv
        └── _evidence/         (93 files)
```

---

## 12. Inspection discipline maintained

| Category | Definition |
|----------|------------|
| Files inventoried | Listed in `all_files.txt` / `tracked.txt` (310 / 298) |
| Files inspected in depth | `FULL_VERBATIM_READ` via read tool (83 skills) |
| Files classified using prior audit | `TARGETED_INSPECTED` based on Phase 1/2 evidence (167 rows) |
| Evidence payloads persisted | 93 files under `_evidence/` |
| Runtime behaviours actually tested | NONE — read-only static analysis |
| Behaviours documented but not verified | Tool named in code ≠ tool installed; MCP named ≠ MCP contracted |

---

*This document is a handoff summary. It does not replace the original Phase 2 and Phase 3
reports, which contain complete evidence, per-file classifications, and confidence ratings.*
