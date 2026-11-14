# CBH Development Methodology Baseline

> **Document ID:** CBH-DM-BASELINE  
> **Version:** 0.1  
> **Revision:** REV2 (2026-11-05)  
> **Lifecycle:** DRAFT — OWNER REVIEW  
> **Authority:** Proposed working baseline; not approved or locked  
> **Prepared:** 2026-11-04; revised 2026-11-05 (REV1); revised again 2026-11-05 (REV2)  
> **Revision history:** REV1 applied F-01–F-14; REV2 applies R-01–R-07.  
> **Applies to:** Development, documentation, review, testing, and repository operations for CBH

---

## Classification key

Every rule in this revision carries one of these labels:

| Label | Meaning |
|---|---|
| **[Confirmed — source]** | Directly supported by the master handoff or the corroborating project-history document included under `source-reference/`. |
| **[Derived]** | Follows from two or more confirmed rules, but is not stated as a single passage in the source. |
| **[Proposed]** | Recommended refinement; not owner-approved and not binding. |
| **[Example]** | Illustration only; not a rule and not a separate source claim. |

An unlabeled statement is explanatory prose, not a rule.

---

## 1. Purpose

This document defines how CBH work is analyzed, designed, reviewed, approved, implemented, and verified. It governs the way the project is developed; it does not define the system architecture or choose which existing CBH components will be retained, changed, merged, or removed.

The methodology is independent of Buggy. Buggy is an external architecture and methodology reference, not the authority for CBH decisions. CBH remains an independent project. This document does not copy Buggy contracts or settle any Buggy source-authority question. **[Confirmed — source: handoff §3 and Phase 4 §2A]**

Shared governance vocabulary — for example `GAP`, `LOCKED`, bounded task, Skill discovery/mapping/loading/execution, and “no prompt treadmill” — does not import Buggy contract text, Buggy authority, or Buggy approval status into CBH. The provenance of each rule is recorded in `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md`. **[Confirmed — source: handoff §3 line 61 and Phase 4 §2A line 1119; derived clarification]**

This is a draft baseline for owner review. It does not authorize repository changes, implementation, Reference Alignment, Phase 4, or any owner lock.

## 2. Project and reference boundaries

**[Confirmed — source: handoff §2 lines 30–47, §3 lines 49–61, §5.1 lines 84–92, Phase 4 §2A–C lines 1115–1253, and non-negotiable rules lines 240–242]**

| Item | Role in the work | Boundary |
|---|---|---|
| CBH | Target product being assessed and developed; built on the current `Claude-BugHunter` base | Final architecture and product decisions belong to the CBH owner; CBH is not a copy of Buggy or Ai-Hunting |
| Claude-BugHunter | Upstream software repository from which the CBH development checkout originated (`~/tools/Claude-BugHunter`; remote `elementalsouls/Claude-BugHunter`) | Its presence does not mean every component will be retained; upstream history and files must not be confused with the CBH working copy |
| Buggy | Independent architecture, runtime, and methodology reference | Selective comparison only; no wholesale copying and no authority over CBH |
| Ai-Hunting | External project reference for Skills, commands, learning, memory, and runtime comparison | A file-tree snapshot alone does not prove execution quality or maturity; do not claim the repository was fully analyzed or run |
| OffsecCyber | External dataset/reference candidate for knowledge, evaluation, or possible training | Do not assume fitness for training, retrieval, or evaluation without provenance, schema, quality, licensing, and leakage checks; do not generalize from a dataset card or small sample to the quality of all data |
| Development Methodology | CBH's own working rules and decision process | Separate from Buggy contracts and from the future Unified System Architecture Blueprint |

Reference material can inform a proposal. It does not become a CBH requirement until the owner approves the relevant decision. **[Confirmed — source: handoff §4.1 line 1305, §11 line 248]**

## 3. Governing principle

**AI proposes → Runtime proves → Human decides.** **[Confirmed — source: handoff §2 lines 1372–1380]**

- AI systems analyze evidence and propose options or changes. **[Confirmed — source: handoff §2]**
- Runtime behavior, tests, and observable artifacts provide evidence only for the specific behavior they exercise. **[Confirmed — source: handoff §2 and §5]**
- The human project owner makes product, architecture, approval, lock, freeze, and reopen decisions. **[Confirmed — source: handoff §1 and §2]**

An AI response is not runtime evidence. A test result is not broader than its test scope. A reviewer recommendation is not owner approval. Silence is not consent. **[Confirmed — source: handoff §1 line 1367, §2 line 1380, §4.1 line 1305]**

## 4. Roles and authority

**Confirmed role responsibilities:** The Owner, Architect/Reviewer, Document Author, and Repository Operator roles and their authority limits are recorded in the handoff. **[Confirmed — source: handoff §1 lines 1363–1370]**

**Derived role model:** The Runtime / Test Environment row is a derived operational role, not a named role in the source table; it is included because the governing principle assigns runtime/tests an evidence-only function. The named current assignments are continuity notes, not permanent authority grants; the owner may change them, and the handoff requires re-checking the available model/provider list before relying on it. **[Derived — source: handoff §2 lines 1372–1380, §5.3 line 121, and Phase 4 §7 line 1341; confirmed role boundaries at §1]**

| Role | Current continuity assignment | Responsibilities | Authority boundary | Basis |
|---|---|---|---|---|
| Project Owner | User | Owns product direction, supplies priorities and source material, approves scope and changes, and decides approval/lock/freeze/reopen | Sole final decision authority. No approval is inferred from silence or an AI recommendation | Confirmed |
| Architect / Reviewer | ChatGPT (recorded continuity assignment) | Analyzes source material, maps dependencies, identifies gaps and conflicts, proposes designs, and reviews deliverables against sources and acceptance criteria | Proposes and reviews; does not claim repository execution or runtime tests it did not perform; cannot approve or lock | Confirmed |
| Document Author | DeepSeek in ChatGPT (recorded continuity assignment) | Produces a bounded document or artifact from specified inputs and an explicit writing brief | Does not choose the next project phase, authorize implementation, or create an owner lock | Confirmed |
| Repository Operator / Executor | OpenCode in Kali (recorded continuity assignment) | Performs authorized repository reads/writes, commands, tests, and explicitly permitted Git operations | Operates only within the approved task and paths; does not independently redesign the system, expand scope, or alter locked artifacts | Confirmed |
| Runtime / Test Environment | Actual execution environment | Produces observable results, test output, logs, and artifacts | Provides evidence, not product approval or policy authority | Derived |

Current assignments are continuity notes, not permanent authority grants. No model or vendor is granted approval authority by this table. **[Derived clarification — source: handoff §1 role boundaries and §5.3 model-list caveat]**

### 4.1 Separation of responsibilities

**Confirmed working boundary:** The Architect/Reviewer analyzes and reviews; the Document Author drafts; the Repository Operator executes only authorized work; the Owner decides. **[Confirmed — source: handoff §1]**

**Confirmed review requirement:** Review is an independent review that compares the candidate with acceptance criteria. **[Confirmed — source: handoff §3 line 1390]**

**Proposed operational refinement — owner review required:** The specific independence threshold — which artifact or task classes require a reviewer distinct from the author — and the detailed separation-of-duty and escalation mechanics remain open. Where practical, the reviewer should use the source material and acceptance criteria independently rather than relying only on the author's self-check. Cross-contract or cross-workstream conflicts should be escalated to the owner instead of being silently resolved while editing another document. These details are recommended here, not yet binding owner-approved rules. **[Proposed — source: traceability §17 item 3; handoff §3 confirms independent review in principle]**

## 5. Official work lifecycle

```text
Analyze → Design → Review → Approve → Implement → Verify
```

**[Confirmed — source: handoff §3 lines 1382–1395]**

No work jumps directly from Analyze to Implement. **[Confirmed — source: handoff §3 line 1395]**

No phase may be skipped merely to save time. **[Derived — from the six-stage lifecycle and the line 1395 prohibition; the source states the jump prohibition, not the motive.]**

### 5.1 Analyze

Purpose: establish what is known before proposing a change.

**Confirmed required work** — source: handoff §3 step 1 (line 1388), non-negotiable rule line 239, and Phase 4 §5 lines 1307–1315:
- Read the relevant source files and existing audit evidence.
- Extract source facts and open GAPs.
- Classify findings using the five source terms: **Source fact**, **Observed behavior**, **Reviewer analysis**, **Decision proposal**, and **Owner decision**.
- Reuse valid prior audit results; do not repeat a full audit without a material reason.

**Derived analysis elaborations** — useful, but not stated as separate step-1 requirements in the source:
- Identify the intended outcome (which may be recorded in the optional Objective field if the owner adopts it), scope, and non-goals.
- Identify dependencies, affected components, conflicts, and evidence limits.

Expected output: a bounded analysis with source references, findings, limitations, and any blocking questions. **[Derived — source: handoff §3 step 1 and §11 report rule]**

### 5.2 Design

Purpose: propose a specific and reviewable solution.

Recommended design brief contents (the core requirement to state dependencies and trade-offs is source-backed; the expanded checklist below is an operational aid for owner review): **[Confirmed core — source: handoff §3 step 2; expanded checklist: Proposed]**
- The problem being addressed and the intended outcome.
- The affected interfaces, files, components, and dependencies.
- Alternatives considered where a meaningful choice exists.
- Trade-offs, risks, compatibility concerns, and migration implications.
- Acceptance criteria and verification approach.
- What remains unchanged and what is explicitly out of scope.

Design is a proposal, not permission to implement it. **[Confirmed — source: handoff §4.1 line 1305]**

### 5.3 Review

Purpose: test the proposal or artifact against its sources and acceptance criteria.

**Confirmed requirement:** Review is a distinct, independent step and compares the candidate with acceptance criteria. **[Confirmed — source: handoff §3 step 3]**

**Proposed review checklist — owner review required:** **[Proposed — source: traceability §3]**
- Read the complete candidate, not only selected excerpts.
- Verify source-derived claims against the cited source material.
- Check consistency with applicable approved decisions and interfaces.
- Check relevant dependencies, boundary conditions, edge cases, and cross-references.
- Distinguish blockers from non-blocking suggestions.
- State what was verified and what could not be verified.

A review disposition is a recommendation. It does not change lifecycle state or grant approval. **[Confirmed — source: handoff §1 role limits and §4.1 line 1305]**

### 5.4 Approve

Purpose: obtain an explicit owner decision before implementation or normative promotion.

**Confirmed requirement:** Approval must be explicit owner approval of the change scope and version. Human owner approval is required before locking a design or starting a wide change. **[Confirmed — source: handoff §3 step 4 line 1391 and non-negotiable rules line 248]**

**Proposed minimum approval record — owner review required:** The following content list is a proposed minimum record for owner confirmation. It does not decide whether approvals must be captured in a dedicated register; that remains open under §17.2.
- The task or artifact being approved.
- The approved scope and allowed change boundary.
- The relevant version or baseline.
- Any limits, conditions, or excluded actions.

**[Confirmed core: scope + version — source: handoff §3 step 4. Proposed: task/artifact identity, limits/conditions, and register format.]**

Approval of one bounded task is not blanket approval for adjacent tasks. **[Derived — source: handoff §3, §4 bounded task, and §6 no automatic scope expansion]**

A reviewer `PASS`, `PASS — READY TO LOCK`, or equivalent is not an owner decision. **[Confirmed — source: handoff §1 Document Author boundary and §4.1 line 1305]**

No implementation begins before explicit approval of the relevant scope. **[Confirmed — source: handoff §3 and non-negotiable rules line 248]**

### 5.5 Implement

Purpose: execute one bounded task within the approved boundary.

**Confirmed implementation rules** — source: handoff §3 step 5, §4 lines 1397–1405, §10 line 1470, and non-negotiable rules:
- Change only the files, paths, and behaviors authorized by the task.
- Preserve unrelated user changes.
- Do not modify a locked artifact within the same version. A normative change requires a successor version and explicit owner approval.
- Do not delete, merge, rename, or move a file solely because an assessment labels it optional, redundant, or a modification candidate.

**Derived implementation safeguards** — reasonable consequences of the bounded-task, source-preservation, and reporting rules:
- Preserve existing source evidence. **[Derived — source: non-negotiable rule line 240 and §7 evidence discipline]**
- Do not add opportunistic cleanup, refactors, migrations, or feature work. **[Derived — source: §4 line 1402 and §8 line 1441]**
- Stop and report when the task cannot be completed within its authorized boundary. **[Derived — source: §11 lines 1474–1481]**

### 5.6 Verify

Purpose: establish what the implementation actually did and did not prove.

The report must identify the commands and tests actually executed, their results, the relevant output/evidence, and the limits of those results. Tests not executed must be marked `NOT RUN` or `NOT VERIFIED`; they must never be represented as passing. **[Confirmed — source: handoff §3 step 6 and §5 lines 1409–1416]**

A successful implementation step does not automatically prove release readiness, runtime safety, or correctness outside the tested scope. **[Confirmed — source: handoff §2 line 1380 and §11 line 1483]**

## 6. Bounded task contract

Every executable task must specify at minimum the six handoff-confirmed fields: **[Confirmed — source: handoff §4 line 1399]**

1. **Source inputs** — exact files, versions, reports, or environment facts to use.
2. **Allowed changes** — explicit files, paths, and permitted operations.
3. **Dependencies** — prerequisites and affected interfaces or tasks.
4. **Outputs** — expected files, reports, artifacts, or behavior.
5. **Acceptance checks** — concrete conditions and tests that determine completion.
6. **Stop conditions** — situations that require execution to stop and be reported.

**Proposed optional field — owner review required:** A one-line **Objective** (one observable outcome) is recommended, but it is not part of the six fields confirmed by the master handoff. It remains optional until separately approved. **[Proposed — see traceability §3 and F-01 in `REVISION_NOTES.md`]**

The following fields are recommended additions for better task reproducibility and are proposed for owner confirmation: task ID, non-goals, repository root/branch/HEAD, risk classification, backup/rollback approach, test environment, expected evidence paths, and commit/push permissions. **[Proposed — source: traceability §3]**

A task must not be broadened silently. If new work is discovered, record it as a separate task or request an explicit scope update. **[Confirmed — source: handoff §6 no automatic scope expansion and §8 one bounded task]**

## 7. Change and artifact control

**Confirmed rules — source: handoff §4 lines 1397–1405, §9 line 1456, and §11 line 1483:**
- A locked artifact is immutable within its locked version.
- A normative change to a locked artifact requires a successor version, a bounded change description, review, and explicit owner approval.
- Do not change more than one major artifact in one task unless the dependency is inseparable and explicitly documented.
- Do not perform a sweeping rewrite or migration without a bounded plan/manifest and owner approval.
- Do not delete, merge, rename, or move a file solely because an assessment labels it optional, redundant, or a modification candidate.
- Do not treat `TODO`, `IN_PROGRESS`, or `DONE` as lock states. These are project progress labels. `LOCKED` is a separate owner decision tied to a specific artifact/version. Do not write `LOCKED` as a lifecycle state unless the contract explicitly allows it. **[Confirmed — source: handoff §9 line 1456]**
- Never place secrets in Git, prompts, logs, or packages.
- Use hashes only against a trusted reference; a hash is not a substitute for trusting the comparison source. **[Confirmed — source: handoff §4 line 1405]**
- File transfer is not implementation. Test pass proves only its scope. Commit/push is not proof of runtime safety.

**Derived safeguards — source: confirmed owner-authority, evidence, and provenance rules:**
- A candidate, reviewer PASS, successful transfer, commit, or checksum does not independently establish owner approval. **[Derived — handoff §1/§2 owner authority, §4.1 line 1305, §9 LOCKED rule, §11 line 1483]**
- A hash does not by itself establish source authenticity or authority. **[Derived — corollary of the trusted-reference rule at line 1405 and the owner-authority rules]**
- Keep source artifacts, generated reports, reconstructed candidates, and derived documents distinguishable. **[Derived — handoff Phase 4 §5 source-vs-inference and Source Register §4]**
- Record provenance and limitations for copied, reconstructed, or generated material. **[Derived — handoff Phase 4 §5 source-vs-inference and exit-gate discipline]**

## 8. Evidence and testing discipline

Every test or verification claim must say what it proves and what it does not prove. **[Confirmed — source: handoff §5 line 1409]**

Proof-boundary examples (illustrations of the rule above; each mirrors a handoff §5 illustration): **[Example — source: handoff §5 lines 1410–1416]**
- A Mock test proves behavior in the Mock configuration only.
- A preflight check does not prove that the actual dispatcher enforces the preflight result.
- A unit test for a validator does not prove that every invocation path passes through that validator.
- Successful report generation does not prove that a finding is valid.
- A module rejecting an out-of-scope request does not prove that all network egress is blocked.
- A passing test for one interface or fixture does not prove correctness of the entire product.

Evidence should be traceable to the relevant task, component, test, finding, target (where applicable), and original request/response or artifact. Keep evidence reproducible where possible and preserve the distinction between mock, local-lab, and live/authorized results. **[Confirmed — source: handoff §5 line 1416]**

Do not claim `PASS` for work that was not executed. Use `NOT RUN`, `NOT VERIFIED`, or another explicit non-pass disposition when appropriate. **[Confirmed — source: handoff §5 line 1415]**

## 9. Scope and safety rules

**Confirmed scope/safety rules** — source: handoff §6 lines 1418–1427. These rules govern security-testing work and any project operation that can affect systems or data.

- Default to deny when authorization or scope is absent, ambiguous, or cannot be established.
- When allow and deny rules conflict, deny takes precedence.
- Do not expand scope automatically from a hostname, redirect, or discovered asset.
- Keep passive collection, active testing, and intrusive testing distinct.
- Destructive or state-changing actions are not default validation methods. They require clear necessity, safe conditions, and appropriate authorization.
- Bound rate, concurrency, timeout, and blast radius when relevant.
- Enforce authorization and tool policy at the actual invocation/runtime boundary; prompt instructions alone are not enforcement.
- A scope validator is not a network sandbox. Runtime isolation and egress controls must be considered separately where required.

**Derived scope-expansion examples:** Treat linked domains and other observed relationships in the same way; they are examples of the no-automatic-expansion principle, not a separate source list. **[Derived — extension of line 1422]**

## 10. Agent and Skill working rules

**Confirmed Skill rules** — source: handoff §7 lines 1429–1437:

- Prefer a small number of clearly bounded agents with a well-organized Skill catalog over creating one agent for every vulnerability class.
- Define Skill ownership boundaries to reduce duplicated probes and routing ambiguity.
- Keep these concepts distinct: **Skill discovery ≠ Skill mapping ≠ Skill loading ≠ Skill execution**.
- Declare required tool capabilities accurately. Do not claim browser proof when no browser execution path exists.
- Skill instructions and commands must be bounded, verifiable, and appropriate to the authorized target and test context.
- Destructive payloads must not be presented as ordinary proof or default validation.
- Skill changes should receive appropriate lint, schema, cross-reference, and safety review, plus appropriate tests.

**Derived Skill safeguards** — reasonable extensions of the confirmed capability-honesty and testing rules:
- Apply the same capability-honesty rule to Burp and other tool-backed proof when the corresponding execution path is unavailable. **[Derived — extension of line 1434]**
- Treat behavior checks as part of the appropriate test expectation. **[Derived — extension of line 1437]**

## 11. No prompt treadmill / efficient reuse

**[Confirmed — source: handoff §8 lines 1439–1446 and non-negotiable rules line 239]**

- Work on one bounded task at a time.
- Reuse valid prior audit results and evidence.
- Do not repeat a complete corpus audit or the same test with identical inputs unless there is a material reason, such as changed sources, a new baseline, a contradiction, or an unmet acceptance criterion.
- When a gap is found, record the exact gap and request only the additional evidence needed.
- Do not generate multiple prompts that seek the same result without a meaningful change in inputs or acceptance criteria.
- Group related decisions by dependency cluster where that reduces duplicated analysis, but keep implementation tasks bounded.

## 12. Progress, status, and decision vocabulary

For project roadmap progress, use: **[Confirmed — source: handoff §9 lines 1448–1456]**

- `TODO`
- `IN_PROGRESS`
- `DONE`

These are progress states only. An artifact's lifecycle state, review disposition, owner approval/lock, repository transfer, implementation status, test status, and runtime verification are separate facts and must not be collapsed into one label.

Do not call an artifact `LOCKED` unless there is an explicit owner decision for that exact artifact/version, and do not write `LOCKED` as a lifecycle state unless the contract explicitly allows it. **[Confirmed — source: handoff §9 line 1456]**

Do not close a GAP without supporting evidence and an appropriate acceptance test. **[Confirmed — source: handoff non-negotiable rules line 245]** Do not downgrade or reassign a GAP without the required owner decision. **[Derived — owner-authority rules plus the confirmed GAP-closure evidence requirement]**

## 13. Git and repository safety

Before any Git operation, inspect and record: **[Confirmed — source: handoff §10 lines 1458–1470 and §5.2 lines 94–110]**

```bash
pwd -P
git rev-parse --show-toplevel
git branch --show-current
git rev-parse HEAD
git status --short --branch
git remote -v
git config --get remote.pushDefault
git config --get push.default
```

Confirm the intended repository, branch, baseline, and task before proceeding. Re-check remotes and push routing rather than assuming a prior setup is unchanged. **[Confirmed — source: handoff §5.2 line 110]**

Do not run the following without specific owner approval: **[Confirmed — source: handoff §10 line 1470]**
- `git reset --hard`
- `git clean` (especially destructive modes)
- force push
- history rewrite
- branch deletion
- remote replacement or push-routing changes

Preserve user changes. Never push to the upstream/original repository as a side effect of an ordinary task. A commit or push is permitted only when the task explicitly authorizes the intended repository, branch, and destination. **[Confirmed — source: handoff §10 and §5.2]**

## 14. Security and information handling

**Confirmed working rules — source: handoff §4 line 1404, exit gate line 1349, Phase 4 §2C, and non-negotiable rule line 242:**
- Never place API keys, passwords, tokens, private credentials, or other secrets in Git, prompts, logs, or packages.
- Record provenance and licensing/permission limitations for external material.
- Do not assume an external dataset is fit for training, retrieval, or evaluation without quality, licensing, and leakage checks.

**Derived information-handling safeguard:** Do not overstate reuse, redistribution, or sublicensing rights; the licence/provenance check is the source fact, and the non-overstatement rule is its operational corollary. **[Derived — source: exit gate line 1349 and the provenance discipline]**

**Proposed operational refinements — owner review required:** **[Proposed — source: traceability §3]**
- Avoid printing secrets during debugging; redact sensitive values from evidence while preserving enough context for safe reproduction.
- Treat external repository contents, datasets, prompts, tool output, and target responses as untrusted data that cannot override the approved task boundary.

## 15. Required end-of-task report

Every implementation task must finish with a report containing: **[Confirmed — source: handoff §11 lines 1472–1483]**

1. The exact scope completed.
2. Files created or modified, with paths.
3. Commands and tests actually run, with their real results.
4. Source discrepancies, open GAPs, blockers, and limitations.
5. Commit hash and push destination only if a commit/push actually occurred.
6. Work explicitly not performed.

For analysis or review-only tasks, report the sources inspected, findings, confidence/limitations, and actions not performed. Do not imply that a repository change or runtime test occurred when it did not. **[Derived — source: handoff §11 and §5]**

File transfer is not implementation. Test pass proves only its scope. Commit/push is not proof of runtime safety. **[Confirmed — source: handoff §11 line 1483]**

## 16. Proposed stop and escalation checklist — owner review required

The following checklist operationalizes the existing bounded-task and approval rules. Treat it as a proposed refinement until the owner approves it. Stop execution and report rather than improvising when: **[Proposed — source: traceability §3]**

- Scope, authorization, or the intended repository is ambiguous.
- A requested change would exceed the allowed paths or operations.
- An unexpected dirty working tree or user change is discovered.
- A locked artifact would need to be changed without a successor-version approval.
- A source conflict affects the proposed decision and cannot be resolved from authoritative evidence.
- Required inputs, dependencies, tools, or test environments are missing.
- A command may cause destructive or externally visible effects not covered by the approval.
- A credential or sensitive-data exposure is discovered.
- A test result contradicts the expected behavior or the evidence is insufficient to support the completion claim.

The Repository Operator must not quietly broaden the task, bypass a missing approval, or invent a result. Escalate the smallest precise blocker to the owner. **[Derived — source: handoff §1, §3, §6, and §11]**

## 17. Open owner decisions for this baseline

The following items are not silently defined by this draft and require owner confirmation if they are to become formal rules: **[Proposed — source: traceability §3]**

1. **Risk/approval matrix:** whether to define risk tiers and the exact approval required for each tier (documentation-only, code change, security-sensitive behavior, intrusive testing, data migration, commit, push, publication).
2. **Approval record format:** whether every approval must be captured in a dedicated decision register, or whether an explicit task-specific approval in the project conversation is sufficient for lower-risk bounded tasks.
3. **Review independence threshold:** which artifact/task classes require a reviewer distinct from the author, beyond the confirmed independent-review step.
4. **Rollback standard:** which task classes require a rollback plan, backup, or recovery test before implementation.
5. **Task ID and evidence naming:** whether to standardize identifiers and artifact paths across all workstreams.
6. **Status vocabulary:** whether to adopt a common test-result and review-disposition vocabulary beyond the explicit `NOT RUN` / `NOT VERIFIED` requirement.

These are proposed governance refinements, not current owner-approved rules.

## 18. Non-goals and phase boundary

The identifiers A-02, A-03, and A-04 are external Buggy authority matters recorded in the Buggy Stage 2 authority reference under `source-reference/`. They are carried as unresolved context, not as CBH methodology rules. **[Confirmed — external context; source: `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` rows A-02–A-04]**

This baseline does not:

- Design or approve the CBH system architecture. **[Confirmed — source: handoff §1 and Phase 4 §8]**
- Decide the disposition of files in the Phase 3 assessment. **[Confirmed — source: handoff §4 table and Phase 3 status]**
- Select or promote Buggy/Ai-Hunting designs for CBH. **[Confirmed — source: handoff §3 and non-negotiable rule line 241]**
- Resolve Buggy authority questions A-02, A-03, or A-04. These remain Buggy owner decisions, not CBH methodology decisions. **[Confirmed — external context; source: `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` rows A-02–A-04]**
- Perform Reference Alignment. **[Confirmed — source: handoff §9 and Phase 4]**
- Start Phase 4, Phase 5, migration, or implementation. **[Confirmed — source: handoff phase table lines 71–72 and non-negotiable rules]**
- Claim repository transfer, tests, commits, pushes, or runtime behavior. **[Confirmed — source: handoff §11 line 1483]**

## 19. Acceptance criteria for this draft

The baseline is ready for owner review when:

- The role boundaries and owner authority are explicit. **[Confirmed — source: handoff §1]**
- The six-step work lifecycle is represented without skipping approval. **[Confirmed — source: handoff §3]**
- Bounded-task requirements and change boundaries are explicit. **[Confirmed — source: handoff §4]**
- Evidence/testing limits are explicit. **[Confirmed — source: handoff §5]**
- Scope/safety, Skill/agent, prompt-efficiency, Git, and reporting rules are included. **[Confirmed — source: handoff §6–§11]**
- Confirmed working rules are distinguishable from derived and proposed refinements. **[Derived acceptance criterion for this revision]**
- No Buggy contract is silently represented as a CBH owner-approved rule. **[Confirmed — source: handoff §3 and Phase 4 §2A]**
- No implementation or later phase is authorized by this document. **[Confirmed — source: handoff §1 and §11]**

**Current disposition: DRAFT — OWNER REVIEW REQUIRED.**
