# REV2 Revision Notes

**Baseline:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md`  
**Document version:** 0.1 (unchanged)  
**Revision label:** REV2 (2026-11-05)  
**Basis:** `CBH-METHODOLOGY-VERIFICATION/DEVELOPMENT_METHODOLOGY_REV1_REVIEW.md` (R-01 through R-07); REV1 findings F-01 through F-14 retained as history.

This revision preserves the baseline's §1–§19 structure and valid content. REV1 applied the fourteen F-findings. REV2 applies only R-01–R-07: it adds provenance for the Buggy A-02/A-03/A-04 descriptions, separates confirmed rules from derived elaborations in the affected sections, and corrects the low-severity citation and wording defects. REV2 does not rewrite the methodology, resolve owner decisions, change the six confirmed task fields, or change the draft status.

## Classification used

- **Confirmed** — directly supported by the master handoff or the corroborating project-history document.
- **Derived** — follows from two or more confirmed rules, or is a reasonable operational elaboration not stated as a single source passage.
- **Proposed** — recommended refinement; not binding.
- **Example** — illustration only.

A rule was **not** demoted merely because the earlier traceability table omitted its supporting source passage. Where the master handoff contained the passage, the rule was reclassified to **Confirmed** and cited. REV2 applies the same discipline in reverse: useful material that is not a literal source rule is retained but labeled **Derived**, rather than presented as confirmed.

---

## REV2 changes (R-01–R-07)

| Finding | Severity | Resolution | Primary evidence |
|---|---|---|---|
| R-01 | Medium | A-02, A-03, and A-04 are now traced to the Buggy Stage 2 authority records. Two Stage 2 evidence files were added under `source-reference/`; the manifest, checksums, provenance, and traceability were updated. The decisions remain unresolved Buggy owner matters, not CBH methodology decisions. | `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` rows A-02–A-04; `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` §4 A-02–A-04 |
| R-02 | Medium | §4, §5, §5.1, §5.5, §9, §10, and §14 now separate directly sourced rules from derived operational elaborations, with per-section labels and a per-row `Basis` column in the §4 table. Useful derived content was retained. | Baseline §§4, 5, 5.1, 5.5, 9, 10, 14; traceability §3.4 |
| R-03 | Low | The §5.6 citation now points to handoff §2 line 1380, not §5 line 1380. | `CBH_COMPLETE_HANDOFF.md` §2 line 1380 |
| R-04 | Low | The §7 source header now includes §9 line 1456. The `TODO`/`LOCKED` rule now matches the source, including the contract-permission condition, and §12 uses the same wording. | `CBH_COMPLETE_HANDOFF.md` §9 line 1456 |
| R-05 | Low | The trusted-reference hash rule remains **Confirmed**; the authenticity/authority corollary is now **Derived**. | `CBH_COMPLETE_HANDOFF.md` §4 line 1405 |
| R-06 | Low | The F-09 revision-note citation now points to Phase 4 §5 lines 1307–1315, with the `.docx` as corroboration. Source Register §4 is identified as a different taxonomy, not the five-term source. | `CBH_COMPLETE_HANDOFF.md` Phase 4 §5 lines 1307–1315; `CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx` |
| R-07 | Low | §5.1 now asks for the intended outcome, noting that it may be recorded in the optional `Objective` field if the owner adopts it. `Objective` remains optional/proposed. | Baseline §§5.1 and 6 |

### R-01 — Buggy A-02/A-03/A-04 provenance

The Buggy Stage 2 package (`BUGGY-REFERENCE-HANDOFF-STAGE2-REVISED.zip`, SHA-256 `042a40e16118a277b74cc4a48d5e62eac6d80578004172631099bcbe6a166ec7`) contains the missing provenance. Its `AUTHORITY_DECISION_QUEUE.md` rows A-02, A-03, and A-04 explicitly state the three matters described in the REV1 traceability section. Its `SOURCE_AUTHORITY_AUDIT.md` §4, A-02–A-04, provides the narrative evidence. Those two files were copied byte-identically into `source-reference/` as:

- `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` — SHA-256 `950956f1cee85276938444c77246c66a95327e6fa6105753dce1ef39dffdd22b`
- `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` — SHA-256 `9c8a1515f118d4a82a289f57e77742b7a4eecdae3ec24c44afd9add539bc03d5`

The queue records:

- **A-02:** Agent Security v1.1 round-3 review is `PASS — READY TO LOCK`; no owner lock record was located; the Context Map says authority is unresolved; the v1.1 candidate is reconstructed from the v1.0 baseline and the round-3 diff. Safe treatment: reconstructed review candidate only; retain v1.0 as historical baseline.
- **A-03:** Model Routing v0.5 body says owner-locked 2026-10-15; the 2026-10-25 Context Map labels it a review candidate; the body says v0.3 was locked while the Context Map says the v0.3 lock record is only PROPOSED; no separate v0.5 lock record was located. Safe treatment: conflicting authority; no normative status assumed.
- **A-04:** Provider Failure Policy v0.1 lock record says LOCKED 2026-10-15 with Test 19 wording adjusted, but the supplied fourth-pass candidate is the fenced policy body only and still says draft/not approved; the exact final locked body was not located. Safe treatment: use the lock record only for its explicit scope/ownership facts; do not use the fourth-pass candidate as the exact final policy.

These are Stage 2 generated summary/audit records, not Buggy contract bodies. They are included only as provenance for the three descriptions. They do not resolve the decisions, transfer Buggy authority to CBH, or make the Buggy artifacts current. The decisions remain with the Buggy owner.

### R-02 — Classification boundaries

The following sections now distinguish source-backed rules from derived operational elaborations:

- **§4:** the four role responsibilities are **Confirmed**; the Runtime/Test Environment row and the named continuity assignments are **Derived**/continuity notes. The table has a `Basis` column.
- **§5:** the six-stage lifecycle and the no-jump rule are **Confirmed**; “no phase may be skipped merely to save time” is **Derived**.
- **§5.1:** reading sources, extracting facts/GAPs, using the five terms, and reusing prior audits are **Confirmed**; the intended-outcome/scope/non-goals and dependency/conflict/evidence-limit analysis are **Derived**.
- **§5.5:** authorized changes, preserving unrelated user changes, no in-place locked-artifact change, and no delete/merge/move are **Confirmed**; preserving source evidence, no opportunistic cleanup/refactors, and stop-and-report are **Derived**.
- **§9:** the scope/safety rules are **Confirmed**; linked-domain and observed-relationship scope examples are **Derived**.
- **§10:** the Skill rules are **Confirmed**; the Burp/other-tool-backed proof extension and behavior checks are **Derived**.
- **§14:** no secrets, provenance/licensing, and dataset-fit checks are **Confirmed**; the non-overstatement of reuse/redistribution/sublicensing rights is **Derived**.

Traceability §3.4 lists the retained derived elaborations explicitly. No useful content was deleted merely to shorten the document.

### R-03 — §5.6 citation

The baseline now cites `CBH_COMPLETE_HANDOFF.md` **§2 line 1380** for the statement that a successful implementation step does not automatically prove release readiness, runtime safety, or correctness outside the tested scope. The earlier “§5 line 1380” reference was wrong; line 1380 is in §2.

### R-04 — Progress vocabulary and LOCKED

The §7 source header now cites §4 lines 1397–1405, **§9 line 1456**, and §11 line 1483. The rule now reads: `TODO`, `IN_PROGRESS`, and `DONE` are progress labels; `LOCKED` is a separate owner decision tied to a specific artifact/version; `LOCKED` is not written as a lifecycle state unless the contract explicitly allows it. §12 was aligned to the same wording. Scope is no longer included as part of the owner-lock condition because the source ties the lock to the artifact and version, with the contract-permission condition controlling lifecycle use.

### R-05 — Hash rule and authority corollary

The **Confirmed** rule is now limited to the source statement: use hashes only against a trusted reference; a hash is not a substitute for trusting the comparison source. The separate statement that a hash does not by itself establish source authenticity or authority is now **Derived**, as a corollary of the trusted-reference rule and the owner-authority rules.

### R-06 — F-09 citation

The F-09 entry below now cites `CBH_COMPLETE_HANDOFF.md` **Phase 4 §5 lines 1307–1315** for the five terms, corroborated by the same section in `CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx`. `Source Register §4` (lines 1629–1638) is noted only as source-vs-analysis separation; it uses a different taxonomy and is not the source of the five terms.

### R-07 — §5.1 objective wording

§5.1 now asks the analyst to identify the **intended outcome**, not a mandatory “task objective.” The text notes that the outcome may be recorded in the optional `Objective` field if the owner adopts it. §6 still lists exactly six confirmed task fields; `Objective` remains proposed and optional.

---

## REV1 historical findings (F-01–F-14)

### F-01 — Six task fields; Objective reclassified as proposed optional

**Change:** Baseline §6 now states that every executable task must specify the **six** handoff-confirmed fields: source inputs, allowed changes, dependencies, outputs, acceptance checks, and stop conditions. **Objective** was moved out of the required list and is now an explicitly **proposed optional** field pending owner approval.

**Source:** `CBH_COMPLETE_HANDOFF.md` §4 line 1399 lists exactly six fields and does not list Objective.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §6; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-02 — Approval-content list labeled as a proposed minimum record

**Change:** Baseline §5.4 now separates:
- **Confirmed:** explicit owner approval of the **change scope and version**; human owner approval before locking a design or starting a wide change; no implementation before approval; reviewer PASS is not owner approval.
- **Proposed:** the fuller minimum approval record (task/artifact identity, limits/conditions) and any dedicated approval register.

**Source:** `CBH_COMPLETE_HANDOFF.md` §3 step 4 line 1391 (“موافقة صريحة على نطاق التغيير والنسخة”); non-negotiable rule line 248; §4.1 line 1305.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §5.4; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-03 — Project boundary traceability expanded with actual evidence

**Change:** The traceability matrix now cites the handoff passages that support the §2 entries:
- **Claude-BugHunter** is the upstream software repository from which the CBH development checkout originated (`CBH_COMPLETE_HANDOFF.md` §1 line 21, §2 line 32, §3 line 56, §5.1 lines 84–92).
- **Ai-Hunting** is an external project reference; a file-tree snapshot does not prove execution quality or maturity (§3 line 58; Phase 4 §2B lines 1159–1202).
- **OffsecCyber** is a dataset/reference candidate; it must not be assumed fit for knowledge-base ingestion, training, retrieval, or evaluation without quality, licensing, and leakage checks; do not generalize from a dataset card or small sample (§3 line 59; Phase 4 §2C lines 1204–1253; non-negotiable rule line 242).
- **Buggy** is a reference, not the decision-maker; CBH remains independent (§3 line 61; Phase 4 §2A line 1119; non-negotiable rule line 241).

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §2; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2.

---

### F-04 — Source-backed change control separated from derived safeguards

**Change:** Baseline §7 now has two labeled groups.

**Confirmed (handoff §4 lines 1397–1405 and §11 line 1483):**
- Locked artifact immutable within its version; normative change requires a successor version.
- No more than one major artifact per task unless the dependency is inseparable and explicitly documented.
- No sweeping rewrite or migration without a bounded manifest/plan and owner approval.
- No delete/merge/rename/move solely because an assessment labels a file optional/redundant.
- No secrets in Git, prompts, logs, or packages.
- Hashes verify byte identity only against a trusted reference.
- File transfer is not implementation; test pass proves only its scope; commit/push is not runtime safety.

**Derived:**
- Candidate status, reviewer PASS, transfer, commit, or checksum does not independently establish owner approval.
- A hash does not by itself establish source authenticity or authority (REV2 split; see R-05).
- Keep source artifacts, generated reports, reconstructed candidates, and derived documents distinguishable.
- Record provenance and limitations for copied/reconstructed/generated material (external-material provenance is itself confirmed by the exit-gate rule).

**REV2 update (R-04, R-05):** the §7 header now also cites §9 line 1456. The hash rule is split: trusted-reference use is **Confirmed**; the authenticity/authority corollary is **Derived**.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §7; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-05 — Scope/safety details traced directly to the master handoff

**Change:** Baseline §9's confirmed core cites handoff §6 lines 1418–1427. This includes the previously untraced details:
- destructive/state-changing operations are not default and require necessity, safe conditions, and appropriate authorization (line 1424);
- rate/concurrency/timeout/blast-radius bounding (line 1425);
- enforcement at the invocation boundary, not just prompt instructions (line 1426);
- scope validator is not a network sandbox (line 1427).

**REV2 update (R-02):** the confirmed core is retained; linked-domain and observed-relationship examples are now separately labeled **Derived**.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §9; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-06 — Skill safeguards traced directly to the master handoff

**Change:** Baseline §10's confirmed core cites handoff §7 lines 1429–1437. This includes:
- destructive payloads must not appear as ordinary proof or default validation (line 1436);
- every Skill update passes lint/schema/cross-reference/safety review and appropriate tests (line 1437);
- bounded, verifiable, target-appropriate commands (line 1435).

**REV2 update (R-02):** the browser example remains **Confirmed**; the Burp/other-tool-backed proof extension and behavior checks are now **Derived**.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §10; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-07 — Dependency-based grouping traced in prompt efficiency

**Change:** Baseline §11 now cites handoff §8 line 1446 (“اجمع القرارات حسب dependency cluster”) and marks the dependency-grouping bullet **Confirmed**. The no-repeat-audit rule is also tied to the non-negotiable rule at line 239.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §11; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-08 — GAP closure evidence requirement separated from derived owner-control wording

**Change:** Baseline §12 now states:
- **Confirmed:** no GAP closure without supporting evidence and an appropriate acceptance test (`CBH_COMPLETE_HANDOFF.md` non-negotiable rule line 245).
- **Derived:** do not downgrade or reassign a GAP without the required owner decision, derived from the owner-authority rules plus the confirmed closure requirement.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §12; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2 and §3.

---

### F-09 — Analysis terminology aligned with the source

**Change:** Baseline §5.1 now uses the five source terms exactly:
1. **Source fact**
2. **Observed behavior**
3. **Reviewer analysis**
4. **Decision proposal**
5. **Owner decision**

The earlier “direct facts / derived findings / assumptions / unknowns” wording was replaced. Baseline §8 now labels its proof-boundary list as **illustrations/examples** of the confirmed rule, while noting that each example mirrors a handoff §5 illustration.

**Source (corrected in REV2 per R-06):** `CBH_COMPLETE_HANDOFF.md` Phase 4 §5 lines 1307–1315; corroborated by the same section in `CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx`. `Source Register §4` lines 1629–1638 supports source-vs-analysis separation but uses a different taxonomy and is not the five-term source.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §5.1 and §8; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2.

---

### F-10 — Traceability rows for §1 and §19; §5.1–§5.6 coverage stated

**Change:** The matrix now has explicit rows for §1 Purpose and §19 Acceptance criteria. A new §2.1 states that §5.1–§5.6 are covered by the §5 lifecycle row plus one row per subsection. A new §2.2 explains that §1 and §19 are framing/derived sections, not separate source-backed rules or owner decisions.

**Files:** `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §2, §2.1, §2.2.

---

### F-11 — Current assignments clarified as continuity notes

**Change:** Baseline §4 now states that the named assignments (ChatGPT, DeepSeek in ChatGPT, OpenCode in Kali) are continuity notes from the recorded project state, not permanent authority grants. It cites the handoff's role table and the requirement to re-check the current model/provider list.

**Source:** `CBH_COMPLETE_HANDOFF.md` §1 lines 1363–1370; §5.3 line 121; Phase 4 §7 line 1341.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §4.

---

### F-12 — Primary sources included under `source-reference/`

**Change:** The three primary sources are now included byte-identically in the package under `source-reference/`:
- `CBH_COMPLETE_HANDOFF.md` — SHA-256 `afd026a0c444d4ca14f90911f7fb5f302175a90221ace87fcb68002ec94856da`
- `CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx` — SHA-256 `e79fc0fb8962599dbe63bf71e9d3240694dcee0efde3dcbabafcecba7208d9b5`
- `نص ملصق(20261103-152241).txt` — SHA-256 `4c2e6a51a3a9c3548dc493ac96cab73a45d7650112cb62e071475c02029cb217`

`source-reference/PROVENANCE.md` records their origin and immutability. The manifest and `SHA256SUMS.txt` cover them. They were copied from `CBH-METHODOLOGY-PRIMARY-SOURCES.zip` (SHA-256 `4a4f80a9104fd0350333fa68caf1b7486d359a09d3f6df0dd673bf02afa48508`) and verified byte-identical.

**REV2 update (R-01):** two Buggy Stage 2 authority files were added under `source-reference/`, with separate provenance and hashes. They are not CBH primary sources.

**Files:** `source-reference/*`; `PACKAGE-MANIFEST.json`; `SHA256SUMS.txt`; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §1 and §6–§7.

---

### F-13 — Phase boundaries explicitly include Phase 5 and migration

**Change:** Traceability §5 now states that the baseline excludes Reference Alignment, Phase 4, **Phase 5**, **migration**, and implementation, citing the phase table (Phase 5 = Implementation Planning & Migration Strategy, NOT STARTED) and the non-negotiable rules. Baseline §18 already listed Phase 5 and migration; the traceability row now matches it.

**Source:** `CBH_COMPLETE_HANDOFF.md` phase table lines 71–72; §9 lines 211–222.

**Files:** `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §5; `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §18.

---

### F-14 — Shared governance vocabulary does not import Buggy authority

**Change:** Baseline §1 now states that shared vocabulary (`GAP`, `LOCKED`, bounded task, Skill discovery/mapping/loading/execution, “no prompt treadmill”) does not import Buggy contract text, Buggy authority, or Buggy approval status. Traceability §1.1 records the same, with citations to the handoff's “Buggy is a reference, not the decision-maker” statement, the non-negotiable no-blind-copy rule, and the conversation record's separation of Buggy from CBH's own methodology.

**Source:** `CBH_COMPLETE_HANDOFF.md` §3 line 61; Phase 4 §2A line 1119; non-negotiable rule line 241; conversation record lines 984 and 1104.

**Files:** `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` §1; `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` §1.1.

---

## Reclassification summary

The independent review flagged several details as untraced because the earlier traceability table omitted them. On reading the supplied primary sources, those details are directly supported and were reclassified to **Confirmed**, not demoted to proposed:

| Detail | Actual source |
|---|---|
| No more than one major artifact per task unless inseparable and explicit | Handoff §4 line 1401 |
| Report generation success does not prove finding validity | Handoff §5 line 1413 |
| Destructive/state-changing not default; rate/concurrency/timeout/blast-radius bounds | Handoff §6 lines 1424–1425 |
| Destructive payloads not ordinary proof; Skill lint/schema/cross-reference/safety checks and tests | Handoff §7 lines 1436–1437 |
| Group decisions by dependency cluster | Handoff §8 line 1446 |
| No GAP closure without evidence and acceptance test | Handoff non-negotiable rule line 245 |
| Claude-BugHunter, Ai-Hunting, OffsecCyber specifics | Handoff §3 lines 56–59; Phase 4 §2A–C |
| File transfer is not implementation | Handoff §11 line 1483 |

The only items left as **Proposed** are those the source does not settle: the optional Objective field, the fuller approval-record format, the expanded design/review checklists, the independence threshold, extra task fields, redaction/untrusted-input controls, the stop/escalation checklist, risk tiers, approval register/IDs, rollback standard, and extra status labels.

## Remaining owner decisions

- The six proposed refinements listed in baseline §17.
- Whether to keep the optional Objective field.
- Whether the fuller approval-record format should be adopted and in what form.
- The review-independence threshold by artifact/task class.
- Buggy A-02, A-03, and A-04 remain unresolved. Their descriptions are now traced to the Stage 2 authority records, but the decisions themselves remain outside this methodology and with the Buggy owner.

No owner decision is made or implied by this revision. REV2 is still `DRAFT — OWNER REVIEW`.
