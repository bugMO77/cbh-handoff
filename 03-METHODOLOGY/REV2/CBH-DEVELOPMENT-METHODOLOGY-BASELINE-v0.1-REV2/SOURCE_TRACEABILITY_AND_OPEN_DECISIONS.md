# Source Traceability and Open Decisions

> Companion to `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` (REV2)  
> Status: DRAFT — OWNER REVIEW  
> Purpose: show where each working rule came from, distinguish confirmed rules from derived safeguards and proposed refinements, and record unresolved boundaries.  
> Revision history: REV1 applied F-01–F-14; REV2 applies R-01–R-07.

## Classification key

| Label | Meaning |
|---|---|
| **Confirmed** | Directly supported by the master handoff or the corroborating project-history document included under `source-reference/`. |
| **Derived** | Follows from two or more confirmed rules; not stated as a single passage in the source. |
| **Proposed** | Recommended refinement; not owner-approved and not binding. |
| **Example** | Illustration only; not a rule. |

## 1. Source set used

The three CBH primary sources are included byte-identically under `source-reference/` and are immutable evidence for this revision. Two Buggy Stage 2 authority-reference files are also included, solely to document the provenance of A-02, A-03, and A-04; they do not transfer Buggy authority to CBH.

| Source | Location | SHA-256 | How it is used |
|---|---|---|---|
| `CBH_COMPLETE_HANDOFF.md` | `source-reference/CBH_COMPLETE_HANDOFF.md` | `afd026a0c444d4ca14f90911f7fb5f302175a90221ace87fcb68002ec94856da` | Primary source for roles, governing principle, six-stage lifecycle, file-change rules, evidence, scope/safety, Skill rules, prompt efficiency, progress vocabulary, Git safety, end-of-task reporting, non-negotiable rules, project boundaries, and Phase 4 reference-source evidence |
| `CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx` | `source-reference/CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx` | `e79fc0fb8962599dbe63bf71e9d3240694dcee0efde3dcbabafcecba7208d9b5` | Corroborating consolidated handoff copy; not treated as a separate approval event |
| `نص ملصق(20261103-152241).txt` | `source-reference/نص ملصق(20261103-152241).txt` | `4c2e6a51a3a9c3548dc493ac96cab73a45d7650112cb62e071475c02029cb217` | Conversation record confirming that Buggy, Ai-Hunting, OffsecCyber, and CBH's own Development Methodology are distinct reference categories |
| `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` | `source-reference/BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` | `950956f1cee85276938444c77246c66a95327e6fa6105753dce1ef39dffdd22b` | Buggy Stage 2 authority-decision summary; used only to document A-02/A-03/A-04 as unresolved external matters |
| `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` | `source-reference/BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` | `9c8a1515f118d4a82a289f57e77742b7a4eecdae3ec24c44afd9add539bc03d5` | Buggy Stage 2 audit narrative §§A-02–A-04; corroborates the queue; not a CBH rule source |

The baseline was drafted from the CBH working-method records. It does not copy the text or authority status of Buggy's own architecture contracts. Buggy materials remain a separate reference set for later evaluation. The two Buggy Stage 2 files above are provenance evidence only; they are not CBH methodology sources and do not resolve the Buggy decisions.

### 1.1 Shared vocabulary is not Buggy authority

Terms such as `GAP`, `LOCKED`, bounded task, Skill discovery/mapping/loading/execution, and “no prompt treadmill” are shared governance vocabulary. Their presence in this methodology does not import Buggy contract text, Buggy authority, or Buggy approval status into CBH. The master handoff states that Buggy is a reference and not the decision-maker, and that CBH remains independent (`CBH_COMPLETE_HANDOFF.md` §3 line 61 and Phase 4 §2A line 1119; non-negotiable rule line 241; conversation record lines 984 and 1104).

## 2. Traceability matrix

Line references are to `source-reference/CBH_COMPLETE_HANDOFF.md` unless stated otherwise.

| Baseline section | Source-backed working rule | Source location | Classification |
|---|---|---|---|
| §1 Purpose | Methodology is separate from architecture; Buggy is a reference, not authority; shared vocabulary does not import Buggy authority | §3 lines 49–61; Phase 4 §2A line 1119; non-negotiable line 241 | Confirmed |
| §2 Project/reference boundaries | CBH is the target built on the `Claude-BugHunter` base; `Claude-BugHunter` is the upstream software repository; Buggy and Ai-Hunting are references, not copies; Ai-Hunting's file tree alone does not prove quality; OffsecCyber requires quality/license/leakage checks and must not be generalized from a dataset card or small sample | §2 lines 30–47; §3 lines 49–61 (project roles at lines 56–59); §5.1 lines 84–92; Phase 4 §2A–C lines 1115–1253; non-negotiable line 242 | Confirmed |
| §3 Governing principle | `AI proposes → Runtime proves → Human decides`; AI response is not runtime proof; a limited test is not whole-system proof; silence is not consent | §1 line 1367; §2 lines 1372–1380; §3 line 1395; §4.1 line 1305 | Confirmed |
| §4 Roles and authority | Owner, Architect/Reviewer, Document Author, Repository Operator roles and boundaries; continuity assignments are recorded but changeable; model/provider list must be re-checked | §1 lines 1363–1370; §2 lines 1372–1380; §5.3 line 121; Phase 4 §7 lines 1332–1341 | Confirmed core; Runtime/Test Environment role and continuity clarification derived |
| §4.1 Separation | Review is an independent step comparing acceptance criteria; owner decides; reviewer is not owner | §1; §3 line 1390; §4.1 line 1305 | Confirmed core; detailed independence threshold proposed |
| §5 Lifecycle | `Analyze → Design → Review → Approve → Implement → Verify`; no jump from Analyze to Implement; Approve = explicit owner approval of change scope and version; Implement = one bounded task; Verify = explicit report of tested and untested | §3 lines 1382–1395 | Confirmed lifecycle; no-skip inference derived |
| §5.1 Analyze | Read sources and audit evidence; extract facts/GAPs; reuse valid prior audits; no full re-audit without material reason; five-term analysis vocabulary | §3 step 1 line 1388; non-negotiable line 239; Phase 4 §5 lines 1307–1315 | Confirmed core; analysis elaborations derived |
| §5.2 Design | Propose a specific decision with dependencies and trade-offs; design is not implementation permission | §3 step 2 line 1389; §4.1 line 1305 | Confirmed core; expanded checklist proposed |
| §5.3 Review | Independent review; compare acceptance criteria; reviewer recommendation is not owner approval | §3 step 3 line 1390; §4.1 line 1305; §1 role boundaries | Confirmed core; detailed checklist proposed |
| §5.4 Approve | Explicit owner approval of change scope and version; human approval before locking design or starting a wide change; reviewer PASS is not owner approval; no implementation before approval | §3 step 4 line 1391; non-negotiable line 248; §4.1 line 1305 | Confirmed core; approval-record format and extra content proposed |
| §5.5 Implement | Execute one bounded task; change only authorized paths; preserve user changes; no opportunistic work; no in-place locked-artifact change; no delete/merge/move from assessment alone; stop and report | §3 step 5 line 1392; §4 lines 1397–1405; non-negotiable rules | Confirmed core; implementation safeguards derived |
| §5.6 Verify | Report commands/tests actually run, results, evidence, and limits; unrun tests are `NOT RUN` / `NOT VERIFIED`; success does not prove release readiness | §3 step 6 line 1393; §2 line 1380; §5 lines 1407–1416; §11 line 1483 | Confirmed |
| §6 Bounded task contract | Every task states source inputs, allowed changes, dependencies, outputs, acceptance checks, stop conditions; task must not be silently broadened | §4 line 1399; §6; §8 | Confirmed (six fields); Objective and extra fields proposed |
| §7 Change and artifact control | Locked versions are not edited in place; normative changes use a successor version; no more than one major artifact per task unless inseparable and explicit; no sweeping rewrite/migration without manifest/plan and owner approval; no delete/merge/move from assessment alone; no secrets; hashes only against a trusted reference; file transfer is not implementation; commit/push is not runtime safety | §4 lines 1397–1405; §9 line 1456; §11 line 1483 | Confirmed core; hash-authority corollary derived |
| §8 Evidence/testing | Test scope limits; Mock ≠ live; preflight ≠ dispatcher enforcement; unrun tests are `NOT RUN` / `NOT VERIFIED`; evidence traceable to finding/target/request/artifact | §5 lines 1407–1416 | Confirmed; examples illustrative |
| §9 Scope/safety | Default-deny; deny-wins; no automatic scope expansion; passive/active/intrusive separation; destructive/state-changing not default; rate/concurrency/timeout/blast-radius bounds; enforcement at invocation boundary; scope validator ≠ network sandbox | §6 lines 1418–1427 | Confirmed core; linked-domain/observed-relationship examples derived |
| §10 Agent/Skill rules | Few agents and a clear Skill catalog; Skill ownership; discovery/mapping/loading/execution distinct; declare tool capabilities accurately; bounded/verifiable commands; destructive payloads not ordinary proof; Skill updates pass lint/schema/cross-reference/safety checks and tests | §7 lines 1429–1437 | Confirmed core; Burp/behavior-check extensions derived |
| §11 Prompt efficiency | One bounded task; reuse evidence; no repeated audit/test without material reason; record exact gap and request only needed evidence; no duplicate prompt chains; group decisions by dependency cluster | §8 lines 1439–1446; non-negotiable line 239 | Confirmed |
| §12 Status vocabulary | `TODO`, `IN_PROGRESS`, `DONE` are progress labels; `LOCKED` is a separate owner decision tied to an exact artifact/version; `LOCKED` is not written as a lifecycle state unless the contract allows it; no GAP closure without evidence and acceptance test | §9 lines 1448–1456; non-negotiable line 245 | Confirmed core; owner-control extension for downgrade/reassign derived |
| §13 Git safety | Inspect repo/branch/HEAD/status/remotes/push routing before Git operations; dangerous operations require specific owner approval; preserve user changes; do not push upstream as a side effect | §10 lines 1458–1470; §5.2 lines 94–110 | Confirmed |
| §14 Information handling | No secrets in Git/prompts/logs/packages; provenance/licensing/permission limits; no dataset fitness assumption without quality/license/leakage checks | §4 line 1404; exit gate line 1349; Phase 4 §2C; non-negotiable line 242 | Confirmed core; non-overstatement safeguard derived; redaction/untrusted-input controls proposed |
| §15 Task report | Report scope, files, executed tests, gaps, commit/push only if performed, work not done; do not imply execution that did not occur | §11 lines 1472–1483 | Confirmed |
| §16 Stop/escalation | Concrete stop/escalation checklist | Derived from §1, §3, §6, §11 | Proposed |
| §17 Open owner decisions | Risk/approval matrix, approval record format, independence threshold, rollback standard, IDs, extended status vocabulary | Recorded as open refinements | Proposed |
| §18 Non-goals | No Reference Alignment, Phase 4, Phase 5, migration, implementation, Buggy decision resolution (A-02–A-04 external context), or architecture approval | Phase table lines 71–72; §9; Phase 4; non-negotiable rules; `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` rows A-02–A-04 | Confirmed boundary; A-02–A-04 external context |
| §19 Acceptance criteria | Draft self-check derived from §§4–18 | Derived from the sections above | Derived acceptance checklist |

### 2.1 Coverage of §5.1–§5.6

The traceability matrix has one lifecycle row for §5 plus one row per subsection (§5.1–§5.6). Each subsection's mandatory work is mapped to the relevant handoff step in §3 and, where applicable, to §4–§7 and §11.

### 2.2 Coverage of §1 and §19

§1 is a framing section: it restates project independence, the draft status, and the shared-vocabulary rule. §19 is a draft acceptance checklist derived from §§4–18. Neither is a separate source-backed rule, and neither creates an owner decision. Both are now explicitly listed above so the matrix has no silent gaps.

## 3. Confirmed rules versus derived safeguards and proposed refinements

### 3.1 Confirmed from the current CBH working-method records

- Owner has final approval authority; silence is not approval. (§1)
- The governing principle is `AI proposes → Runtime proves → Human decides`. (§2)
- The formal lifecycle has six stages: Analyze → Design → Review → Approve → Implement → Verify; implementation does not begin before approval; there is no jump from Analyze to Implement. (§3)
- Review is an independent step that compares the candidate with acceptance criteria. (§3)
- Approval is explicit owner approval of the change scope and version. (§3.4)
- Every task identifies source inputs, allowed changes, dependencies, outputs, acceptance checks, and stop conditions (six fields). (§4)
- A task must not change more than one major artifact unless the dependency is inseparable and explicitly documented. (§4)
- Locked artifacts are not modified in place; normative changes use a successor version. (§4)
- Sweeping rewrites or migrations require a bounded manifest/plan and owner approval. (§4)
- Files are not deleted, merged, renamed, or moved solely because an assessment labels them optional or redundant. (§4)
- No secrets in Git, prompts, logs, or packages. (§4)
- Hashes are useful only against a trusted reference. (§4)
- Tests must state their proof boundaries; unrun tests are not PASS. (§5)
- Security testing is default-deny under missing/ambiguous scope, deny-wins, and does not automatically expand scope. (§6)
- Destructive/state-changing operations are not default and need necessity, safe testing, and appropriate approval. (§6)
- Rate, concurrency, timeout, and blast radius are bounded when relevant. (§6)
- Enforcement happens at the invocation/runtime boundary; prompt instructions are not enforcement. (§6)
- A scope validator is not a network sandbox. (§6)
- Skill discovery, mapping, loading, and execution are distinct. (§7)
- Few agents and a clear Skill catalog; Skill ownership boundaries; capability honesty; bounded/verifiable commands; destructive payloads not ordinary proof; Skill updates pass lint/schema/cross-reference/safety checks and tests. (§7)
- One bounded task at a time; reuse previous evidence; no repeated audit/test without material reason; group decisions by dependency cluster. (§8)
- Progress uses TODO / IN_PROGRESS / DONE; LOCKED is a separate owner decision tied to an exact artifact/version and is not written as a lifecycle state unless the contract allows it. (§9)
- No GAP closure without evidence and an appropriate acceptance test. (Non-negotiable rules)
- Git state and push routing are inspected before Git operations; dangerous operations require specific owner approval. (§10)
- Each executable task ends with an evidence-based report; file transfer is not implementation; test pass proves only its scope; commit/push is not runtime safety. (§11)
- Buggy is a reference, not the decision-maker; CBH remains independent; Buggy/Ai-Hunting are not to be copied blindly. (§3 and Phase 4 §2A)
- OffsecCyber is not assumed fit for training/retrieval/evaluation without quality, licensing, and leakage checks; do not generalize from a dataset card or small sample. (Phase 4 §2C; non-negotiable rules)
- No guessing at versions or outputs that were not provided. (Non-negotiable rules)

### 3.2 Derived safeguards

These follow from two or more confirmed rules and are labeled `[Derived]` in the baseline:

- Candidate status, reviewer PASS, successful transfer, commit, or checksum does not by itself establish owner approval.
- A hash does not by itself establish source authenticity or authority. (§4)
- Keep source artifacts, generated reports, reconstructed candidates, and derived documents distinguishable.
- Record provenance and limitations for copied, reconstructed, generated, or externally sourced material (external-material provenance itself is confirmed).
- Approval of one bounded task is not blanket approval for adjacent tasks.
- Do not downgrade or reassign a GAP without the required owner decision.
- The stop/escalation checklist in §16 synthesizes existing bounded-task and approval rules.
- Continuity assignments are not permanent authority grants.
- The analysis expected output in §5.1 is a bounded, source-referenced report.
- The no-skip inference, Runtime/Test Environment role, analysis elaborations, implementation safeguards, scope examples, Skill extensions, and non-overstatement safeguard are derived augmentations, listed in §3.4.

### 3.4 Derived operational elaborations retained in REV2

The following are useful operational details but are not literal source rules; they are labeled `Derived` in the baseline and are retained rather than deleted:

- No phase may be skipped merely to save time (§5).
- Intended outcome/scope/non-goals and dependency/affected-component/conflict/evidence-limit analysis (§5.1).
- Runtime / Test Environment role row (§4).
- Preserve existing source evidence; no opportunistic cleanup/refactors; stop and report (§5.5).
- Linked-domain and observed-relationship scope examples (§9).
- Burp/other tool-proof extension and behavior checks (§10).
- Non-overstatement of reuse, redistribution, or sublicensing rights (§14).
- Hash authenticity/authority corollary (§7).

### 3.3 Proposed refinements requiring owner approval

- Expanded design-brief checklist.
- Detailed review checklist.
- Additional separation-of-duty and escalation mechanics beyond the confirmed independent-review step.
- The specific independence threshold by artifact/task class.
- Additional task-envelope fields, including the optional Objective field and the eight extra fields listed in §6.
- Secret-redaction and untrusted-input handling controls beyond the confirmed no-secret/provenance rules.
- Concrete stop/escalation checklist (§16).
- Formal risk tiers and approval matrix.
- Dedicated approval register, uniform task/evidence identifiers, and the approval-record format.
- Universal rollback/backup standard.
- Additional test and review status labels.

These refinements are visibly identified as proposed in the baseline and must not be treated as binding until the owner approves them.

## 4. Related unresolved Buggy authority matters

The A-02, A-03, and A-04 descriptions below are traceable to the included Buggy Stage 2 authority records. They remain unresolved Buggy owner decisions, not CBH methodology decisions. The included evidence files are Stage 2 generated summary/audit records, not Buggy contract bodies; they summarize the supplied Buggy source captures. The underlying Stage 2 files referenced by those records are `sources/security/agent-security.v1.1-round3-independent-review.md`, `sources/security/agent-security.v1.1.review-candidate.reconstructed.md`, `sources/security/agent-security.v1.0.baseline.md`, `sources/security/agent-security.v1.0-to-v1.1-round3.diff`, `sources/governance/BUGGY-ARCHITECTURE-CONTEXT-MAP-2026-10-25.md`, `sources/runtime/model-routing.v0.5.conflicting-status.md`, `sources/runtime/provider-failure-policy.v0.1-lock-record.md`, and `sources/runtime/provider-failure-policy.v0.1.fourth-pass-candidate.md`; they remain in the Stage 2 package and are not reproduced here. Exact citations follow.

- **A-02 — Agent Security v1.1 current authority:** `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md`, row A-02; corroborated by `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` §4, A-02. The v1.1 round-3 review is `PASS — READY TO LOCK`; no owner lock record was located; the Context Map says the authoritative version is unresolved; the v1.1 candidate is reconstructed from the v1.0 baseline plus the round-3 diff. Safe treatment: keep v1.1 as a reconstructed review candidate; retain v1.0 as the historical baseline; do not treat v1.1 as locked or production. Required owner action: confirm whether v1.1 is current and whether a lock decision exists outside the supplied files.
- **A-03 — Runtime Model Routing v0.5 status conflict:** `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md`, row A-03; corroborated by `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` §4, A-03. The v0.5 body says owner-locked 2026-10-15; the 2026-10-25 Context Map labels v0.5 as a review candidate. The same body says v0.3 was locked, while the Context Map says the v0.3 lock record is only PROPOSED; a separate v0.5 lock record was not located. Safe treatment: treat the status as conflicting; assume no normative status. Required owner action: confirm whether the embedded lock statement is the final owner decision and, if it exists, identify the separate lock record.
- **A-04 — Provider Failure Policy v0.1 exact final locked body unavailable:** `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md`, row A-04; corroborated by `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` §4, A-04. The lock record says LOCKED 2026-10-15 with Test 19 wording adjusted, but the supplied fourth-pass candidate is the fenced policy body only and still says draft/not approved. The exact final locked body was not located. Safe treatment: keep the lock-record facts; do not use the fourth-pass candidate as the exact final policy. Required owner action: supply or identify the final locked body, or explicitly accept that the detailed policy body is unavailable for alignment.

This document does not select or promote any of those Buggy artifacts. The master handoff treats Buggy as a reference, not a decision source, and the baseline's §18 lists these as non-goals. Adding the Stage 2 evidence files does not make the Buggy decisions, and does not transfer Buggy authority to CBH.

## 5. Phase boundary

The baseline excludes Reference Alignment, Phase 4, Phase 5, migration, and implementation. The master handoff records Phase 4 as **NOT STARTED** and Phase 5 (Implementation Planning & Migration Strategy) as **NOT STARTED** and dependent on an approved Blueprint (`CBH_COMPLETE_HANDOFF.md` phase table lines 71–72), and it requires Reference Intake and Alignment Review before Phase 4 (`CBH_COMPLETE_HANDOFF.md` §9 lines 211–222). This is stricter than the earlier traceability row, which mentioned only Phase 4.

## 6. Source availability

The three CBH primary sources and the two Buggy Stage 2 authority records are now present locally under `source-reference/` and are included byte-identically in the package. Direct source-file comparison is therefore possible for this revision. The earlier OpenCode verification round, which did not have these files, correctly marked its primary-source comparisons `NOT LOCALLY VERIFIABLE`; that limitation no longer applies to the REV2 package. The two Buggy Stage 2 files are generated authority summary/audit records, used only as provenance for A-02–A-04; they are not Buggy contract bodies and not CBH rule sources.

`source-reference/` files are immutable evidence. They must not be edited, rewritten, or replaced. Any change to them would invalidate the package's traceability and checksums.

## 7. Source integrity

The SHA-256 values in §1 match the files under `source-reference/` and the checksums in `SHA256SUMS.txt`. The package manifest records the same values. `REVISION_NOTES.md` maps the REV1 findings (F-01 through F-14) and the REV2 findings (R-01 through R-07) to the corresponding changes.
