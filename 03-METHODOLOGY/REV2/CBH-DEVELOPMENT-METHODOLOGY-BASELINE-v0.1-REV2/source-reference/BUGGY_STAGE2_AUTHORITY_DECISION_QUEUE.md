# Buggy Authority Decision Queue

**Purpose:** Owner decisions and source limitations to preserve before any CBH Reference Alignment. This file does not make decisions on the owner's behalf.

| ID | Question / limitation | Evidence | Current safe treatment | Required owner action |
|---|---|---|---|---|
| A-02 | Is `agent-security.md` v1.1 the intended current architecture source? | v1.1 round-3 review = PASS — READY TO LOCK; no owner lock record; Context Map says authority unresolved; candidate is reconstructed from baseline + diff | Keep v1.1 as reconstructed review candidate; retain v1.0 as historical baseline | Confirm whether to use v1.1 as current reference and whether a lock decision exists outside supplied files |
| A-03 | Is `runtime/model-routing.md` v0.5 locked or still a review candidate? | v0.5 body says owner-locked 2026-10-15; 2026-10-25 Context Map labels it review candidate; the same body says v0.3 was locked while the Context Map says the v0.3 lock record is only PROPOSED; separate v0.5 lock-record file not located | Treat as conflicting authority; no normative status assumed | Confirm whether the embedded lock statement is the final owner decision; provide/identify separate lock record if one exists |
| A-04 | Where is exact final locked body for `runtime/provider-failure-policy.md` v0.1? | Lock record says LOCKED 2026-10-15 and Test 19 wording adjusted; supplied fourth-pass candidate is the fenced policy body only and still says draft/not approved | Use lock record only for its explicit scope/ownership facts; do not use fourth-pass candidate as exact final policy | Supply/identify final locked body, or explicitly accept that detailed policy body is unavailable for this alignment |
| A-01 | Does v1.3 Agent Architecture Rules ever supersede v1.2? | Reconciliation withdraws prior lock; v1.2 remains production, v1.3 NOT LOCKED; v1.3 body absent | Use v1.2; treat v1.3 materials as history/review evidence | No immediate action unless a later authoritative v1.3 body/owner decision exists |
| A-07 | Is Validation Model v1.1 to be promoted beyond review candidate? | Independent review says PASS — READY TO LOCK, not locked; no owner lock record located | Keep as candidate | Owner lock decision only if the project owner intends it; not required merely to use it as a candidate reference |
| A-09 | Correct registry count? | JSON has `tools` object with 70 entries and `runtime_components` object with 9 entries | Record 79 total: 70 tools + 9 components | No decision; this is a factual count correction |

## Scope note

A-05 (roadmap still references `file-contracts.md` v1.3), A-06 (Tool Manifest lifecycle header predates lifecycle/lock separation), and A-08 (a policy lock does not prove runtime operation) are documentation caveats, not omitted owner decisions. They are recorded and handled in `SOURCE_AUTHORITY_AUDIT.md` and `KNOWN_SOURCE_CONFLICTS.md`; no owner action is requested for them.

## Decision discipline

- Reviewer `PASS` is not owner approval.
- A previous lock claim withdrawn by reconciliation is not an active lock.
- A lock applies only to the exact artifact/version/scope.
- Missing exact bodies are not reconstructed from summaries unless the reconstruction is explicitly labeled and independently hash-checked.
- Do not alter the source documents during this decision pass.
