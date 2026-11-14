# Buggy Source Authority Audit

**Prepared:** 2026-11-04  
**Audit status:** Preliminary source-based audit; independent OpenCode verification completed 2026-11-04 (report maintained separately); owner review pending.  
**Scope:** Authority, version, lock, lifecycle, provenance, and permitted-use classification of the Buggy reference material in this handoff.  
**Out of scope:** Buggy repository audit, Buggy implementation changes, CBH implementation, Reference Alignment, closure of Buggy GAPs, or any Phase 4 design decision.

## 1. Executive result

The supplied Buggy reference set is usable for downstream CBH comparison, but it is **not one uniformly approved specification set**. It contains:

- a locked structural Blueprint;
- locked root/process/architecture contracts;
- a production baseline for Agent / Skill / Command semantics;
- several review candidates that are not owner-locked;
- runtime policies that are document-locked but explicitly not proof of runtime enforcement;
- management summaries whose status statements must be checked against exact artifact and lock evidence;
- two material authority ambiguities and one missing exact locked document body.

**Recommended handling for CBH:** only use artifacts classified below as `LOCKED` or `PRODUCTION_BASELINE` as established Buggy reference baselines, and even then only within their stated scope. Use review candidates as non-binding design evidence. Carry unresolved items as unresolved. Do not infer repository presence, test execution, or runtime readiness from a document lock.

This report is an analytical audit of supplied source files, not a new owner lock or a change to any Buggy artifact.

## 2. Authority rules applied

The audit applies the following source hierarchy, based on the supplied Blueprint, `file-contracts.md` v1.4, and `review-discipline.md` v0.2:

1. **Explicit owner decision for the exact artifact/version/scope.** An approval or lock applies only to the named artifact and scope. Silence and reviewer verdicts are not owner approval.
2. **Exact lock record plus matching artifact bytes**, where available. A lock record establishes the document/policy state, not repository transfer or runtime operation.
3. **Locked canonical Blueprint v4.0** for intended structure, capability catalog, ownership boundaries, build sequence, and repository discipline. It does not lock every downstream contract.
4. **Current production/locked contract versions** for their own defined subject matter.
5. **Review candidates and independent-review reports** as proposals/evidence only. `PASS — READY TO LOCK` is not a lock.
6. **Management artifacts** (roadmaps, handoffs, context maps, prompts, summaries) are navigation/reconciliation aids. They do not silently supersede exact owner decisions or governing contracts.
7. **Reconstructed or transcript-extracted content** must remain labeled as such and must not be represented as an exact standalone original.

Always keep these states separate: lifecycle `Status`, owner lock decision, repository transfer, test execution, implementation, and runtime verification.

## 3. Artifact dispositions

### 3.1 Canonical structure and governance

| Artifact | Evidence in package | Audit disposition | Permitted use |
|---|---|---|---|
| `BUGGY-FINAL-CANONICAL-BLUEPRINT-v4.0.md` | Explicit owner LOCKED decision dated 2026-10-15 in the document | **LOCKED — structural baseline** | Use for intended project shape, catalogs, ownership, build order, and repository workflow. Do not infer implementation or GAP closure. |
| `architecture/file-contracts.md` v1.4 | Separate owner lock record dated 2026-10-24; included body SHA-256 matches lock-record SHA exactly | **LOCKED — current root contract** | Use for file ownership, lifecycle, source-of-truth, paths, and change semantics. v1.3 is historical. |
| `architecture/review-discipline.md` v0.2 | Explicit owner lock in body and separate lock record dated 2026-10-13 | **LOCKED — process governance** | Use for Builder / Reviewer / Architect / Owner boundaries, review independence, bounded corrections, approvals, locks, and truthful status claims. |
| `architecture/agent-architecture-rules.md` v1.2 | Supplied full body says `production v1.2`; later reconciliation preserves it as production baseline | **PRODUCTION BASELINE** | Use as current approved Agent / Skill / Command semantics in the supplied source set. |
| `architecture/agent-architecture-rules.md` v1.3 | Change report plus prior lock record and later lock-reconciliation record; full v1.3 body absent | **REVIEW CANDIDATE — NOT LOCKED** | Use only to understand proposed bounded corrections and its GAP mapping. Do not use as the active contract baseline. |
| `architecture/model-routing.md` v0.1 | Explicit lock record dated 2026-10-13; lifecycle remains `draft` | **LOCKED — architecture-level only** | Use for model-routing philosophy and boundaries. It has no operational model IDs, routing algorithm, or runtime enforcement. |

### 3.2 Architecture review candidates

| Artifact | Evidence in package | Audit disposition | Permitted use |
|---|---|---|---|
| `validation-model.md` v1.1 | Full review candidate; independent review says `PASS — READY TO LOCK (not locked)`; no owner lock record located | **REVIEW CANDIDATE** | Use for validation concepts and candidate requirements; retain GAP-VM-01..10 and do not call it locked. |
| `knowledge-flow.md` v1.1 | Full review candidate; GAP-KF entries remain open; no owner lock evidence located | **REVIEW CANDIDATE** | Use as candidate knowledge-layer model, with provenance and lifecycle gaps visible. |
| `learning-flow.md` v1.1 | Full review candidate; GAP-LF entries remain open; no owner lock evidence located | **REVIEW CANDIDATE** | Use as candidate learning/memory-flow model, not an approved implementation contract. |
| `agent-security.md` v1.0 | Original supplied baseline | **HISTORICAL BASELINE** | Use to trace the v1.1 changes and understand the original threat-model content. Do not silently choose it as the current approved revision. |
| `agent-security.md` v1.1 | Reconstructed from v1.0 baseline + round-3 diff; reconstructed SHA matches the round-3 independent-review candidate SHA; review says `PASS — READY TO LOCK`; no owner lock record found | **RECONSTRUCTED REVIEW CANDIDATE — NOT LOCKED** | Use only as a candidate threat-model update. Authority/current version requires owner reconciliation. |

### 3.3 Runtime policy and inventory

| Artifact | Evidence in package | Audit disposition | Permitted use |
|---|---|---|---|
| `runtime/tool-manifest.md` v1.5 | Full locked policy body plus separate owner lock record; body SHA matches lock-record SHA | **LOCKED — POLICY ONLY** | Use as the supplied tool-gating / approval / MCP / integrity policy. It explicitly says GAP-TM-11 remains OPEN and policy default is refuse-all while open. This is not evidence that runtime enforces it. |
| `runtime/registry.json` v0.7-rev2 | Production JSON and lock record; SHA matches; strict JSON parse succeeds | **LOCKED / PRODUCTION — INVENTORY ONLY** | Use as an inventory snapshot. It contains **70 tools + 9 runtime components = 79 entries**. The declared registry schema is absent; schema validation was not performed. It is not a complete canonical tool-definition source. |
| `runtime/redaction.md` v1.2 | Full locked policy body plus separate lock record; body SHA matches lock-record SHA | **LOCKED — POLICY ONLY** | Use for redaction/restoration/quarantine policy. GAP-AS-02, GAP-AS-08, GAP-TM-17, and GAP-TM-11 remain open; no runtime enforcement is claimed. |
| `runtime/model-routing.md` v0.5 | Full body explicitly contains a 2026-10-15 owner-lock statement and says v0.5 is current locked baseline; the same body's version line also says v0.3 was LOCKED on 2026-10-15 while the Context Map says the v0.3 lock record is only PROPOSED; separate v0.5 lock-record file was not located; 2026-10-25 Context Map labels v0.5 a review candidate | **CONFLICTED AUTHORITY — OWNER RECONCILIATION REQUIRED** | Do not treat as definitive normative policy until the conflict is resolved. The body is useful for candidate operational routing information, with operator-reported evidence clearly labeled. |
| `runtime/provider-failure-policy.md` v0.1 | Separate owner lock record says LOCKED on 2026-10-15; exact final locked body unavailable; included fourth-pass body is explicitly pre-lock/draft and differs in authority/status language; that candidate is only the first fenced Markdown block, and the transcript's Test Plan/Change-Scope section is outside the fence and not included | **LOCK EVIDENCE EXISTS; EXACT LOCKED BODY MISSING** | Use the lock record only for ownership/boundary facts it explicitly establishes. Do not cite the fourth-pass candidate as the final locked contract or copy its detailed rules as approved. Do not merge the transcript's out-of-fence Test Plan into the policy. |

### 3.4 Management and continuity documents

| Artifact | Audit disposition | Permitted use |
|---|---|---|
| `BUGGY-ARCHITECTURE-CONTEXT-MAP-2026-10-25.md` | Management/review artifact; not an owner lock record | Use as a status reconciliation aid, but verify each claim against exact documents and lock records. It contains the v0.5 runtime-routing status conflict. |
| `BUGGY-BUILD-ROADMAP-v4.0.md` | Management/phase-order aid | Use for planned intake/build order. Its Phase 1 list still says file-contracts v1.3; this is stale relative to the v1.4 lock record. |
| `BUGGY-CHAT-HANDOFF-AND-DECISIONS.md` | Process and continuity aid | Use for recorded workflow decisions, subordinate to exact owner decisions and current contracts. |

### 3.5 Raw source captures

| Artifact | Evidence in package | Audit disposition | Permitted use |
|---|---|---|---|
| `sources/source-captures/نص ملصق(20261015-084301).txt` | Raw Arabic paste capture containing the fourth-pass fenced policy body plus an out-of-fence Test Plan (18 numbered tests) and Change-Scope section | **RAW_SOURCE_CAPTURE — NOT AN AUTHORITY ARTIFACT** | Use for provenance and traceability only. Do not treat it as an authority source, a contract, or a substitute for the unavailable final locked body. |

## 4. Material discrepancies and limitations

### A-01 — Agent Architecture Rules v1.3 lock claim was invalidated

An included historical lock record says v1.3 was LOCKED. The later reconciliation explicitly withdraws that claim because the owner's no-open-GAP condition was not met. v1.2 remains the production baseline; v1.3 is not locked. The full v1.3 body is not present in this handoff.

**Treatment:** Use v1.2 as the active baseline. Retain v1.3 artifacts solely as review/history evidence.

### A-02 — Agent Security v1.1 is not owner-locked

The round-3 review passes the candidate as ready to lock, but explicitly says that review does not lock the document. The current Context Map says the authoritative version is unresolved. The v1.1 file here is reconstructed, although its SHA matches the review's candidate SHA.

**Treatment:** Carry v1.1 as a reconstructed review candidate. Do not claim it is locked or production. Owner decision is required before treating it as current normative source.

### A-03 — Runtime Model Routing v0.5 has conflicting status evidence

The v0.5 document itself contains an explicit owner-lock statement dated 2026-10-15 and says it is the current locked baseline. The 2026-10-25 Context Map instead categorizes v0.5 as a review candidate. A separate v0.5 lock-record artifact was not located in this source set. In addition, the same v0.5 body's version line says v0.3 was LOCKED on 2026-10-15, while the Context Map says the v0.3 lock record is only PROPOSED pending owner lock. That is a second layer of the same conflict.

**Treatment:** Do not settle this based on chronology alone. Open an owner-reconciliation item. Until then, use v0.5 only as a candidate source for operational facts, not as an uncontested normative authority.

### A-04 — Provider Failure Policy v0.1 locked body is unavailable

The lock record establishes a lock decision and describes the subject/ownership boundary, but the exact final body is unavailable. The included fourth-pass candidate remains labeled draft/not approved and precedes a final Test 19 wording adjustment. The packaged candidate is only the first fenced Markdown block of the raw transcript; the transcript's Test Plan (18 numbered tests) and Change-Scope section are outside the fence and are not included. They were not merged into the policy.

**Treatment:** Keep the lock-record facts, but do not treat the candidate body as the exact locked policy. Detailed requirements remain unavailable for source-exact comparison.

### A-05 — Roadmap v4.0 contains stale file-contract version reference

The roadmap Phase 1 list calls for file-contracts v1.3. The later v1.4 lock record and matching artifact hash identify v1.4 as the current locked root contract.

**Treatment:** Use v1.4 as the current root contract. Keep the roadmap unchanged as historical management material.

### A-06 — Tool Manifest v1.5 status header predates lifecycle/lock separation

The v1.5 header uses `Status: LOCKED`. Later v1.4 file-contracts and review-discipline v0.2 make clear that lifecycle status and owner lock are separate, and `LOCKED` is not a lifecycle state.

**Treatment:** Treat v1.5 as owner-locked policy because its lock record says so. Do not interpret the header as a runtime status or readiness state. Do not silently edit the locked file.

### A-07 — Validation Model v1.1 review verdict is not a lock

The independent review says `PASS — READY TO LOCK (not locked)`. No separate owner lock record was located.

**Treatment:** Keep as a review candidate. Do not promote it to approved baseline.

### A-08 — Locked policies do not prove runtime operation

Tool Manifest v1.5, Redaction v1.2, Registry v0.7-rev2, and the provider failure policy lock record expressly separate policy/document lock from implementation, transfer, tests, and runtime verification. Tool Manifest says refuse-all while GAP-TM-11 is open.

**Treatment:** Compare the policy design to CBH, but do not infer that Buggy's runtime actually enforces it. For CBH, distinguish desired invariant from verified control.

### A-09 — Registry count correction

The registry contains 70 tool objects and 9 runtime-component objects, for 79 total inventory entries. Any summary that calls this 70 combined tool/component entries is inaccurate.

**Treatment:** Report the two counts separately: 70 tools, 9 runtime components, 79 total entries.

## 5. Hash and structural checks performed in this audit

The following checks were repeated locally against the supplied package bytes:

| Check | Result |
|---|---|
| Original Stage 1 handoff checksum entries | 41/41 pass |
| Updated Stage 2 package checksum entries | 44/44 pass |
| `file-contracts.md` v1.4 body vs lock-record SHA | Exact match |
| `runtime/tool-manifest.md` v1.5 body vs lock-record SHA | Exact match |
| `runtime/registry.json` v0.7-rev2 body vs lock-record SHA | Exact match |
| `runtime/redaction.md` v1.2 body vs lock-record SHA | Exact match |
| Reconstructed `agent-security.md` v1.1 vs round-3 review candidate SHA | Exact match |
| Registry JSON parsing | Pass |
| Registry inventory structure | 70 tools + 9 runtime components = 79 entries |

These are local byte/hash/structure checks only. They do not establish the source repository's current state or runtime behavior.

## 6. Requirements for any later CBH alignment

1. Cite the exact Buggy path and version for every adopted principle.
2. Cite whether the source is locked, production, review candidate, historical, reconstructed, or unresolved.
3. Separate the invariant from Buggy's specific implementation choice. CBH may adopt the invariant without cloning the implementation.
4. Add a CBH-specific rationale and trade-off for `Adopt`, `Adapt`, `Reject`, or `New Design`.
5. Distinguish policy requirements from implementation evidence and tests.
6. Preserve all source GAP IDs and statuses; do not claim closure because a principle is described elsewhere.
7. If an artifact is review-only, reconstructed, missing its locked body, or has conflicting authority, label every downstream use accordingly.
8. Do not copy Buggy repo contents, runtime configs, models, target data, memory, or scripts into CBH automatically.

## 7. Audit exit status

**Preliminary source-authority classification: COMPLETE for the files present in this handoff.**  
**Independent OpenCode verification: COMPLETED 2026-11-04 (report maintained separately); owner review pending.**  
**Owner decisions still required:** A-02 Agent Security v1.1 current authority; A-03 Runtime Model Routing v0.5 status conflict. A-04 exact locked Provider Failure Policy body remains unavailable in this package.  
**Reference Alignment: NOT STARTED.**  
**Phase 4: NOT STARTED.**

Do not advance to the unified baseline until OpenCode has checked the artifact inventory, exact versions, embedded owner-lock statements, lock records, and reported hashes against the package itself. OpenCode may report discrepancies but must not silently repair or reclassify sources.
