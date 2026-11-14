# CBH Development Methodology Baseline — v0.1 REV2 Draft

This is a standalone, owner-review draft describing how CBH work is governed and executed. It is intentionally separate from Buggy's architecture/reference documents and from the future CBH Unified System Architecture Blueprint.

**State:** `DRAFT — OWNER REVIEW`. This package is not an owner-approved or locked contract and grants no implementation permission. Revision REV2 applies the independent REV1 review corrections R-01 through R-07; document version remains 0.1.

## Files

- `DEVELOPMENT_METHODOLOGY_BASELINE_v0.1.md` — the draft working methodology, REV2.
- `SOURCE_TRACEABILITY_AND_OPEN_DECISIONS.md` — source mapping, confirmed/derived/proposed classification, A-02/A-03/A-04 provenance, and unresolved boundaries.
- `REVISION_NOTES.md` — maps F-01 through F-14 and R-01 through R-07 to the corresponding changes.
- `OPENCODE-VERIFY-PROMPT.md` — read-only independent review instructions for DeepSeek V4.1 in OpenCode.
- `source-reference/` — immutable evidence:
  - `CBH_COMPLETE_HANDOFF.md`
  - `CBH_PROJECT_HISTORY_AND_PHASE_REPORTS_2026-11-03.docx`
  - `نص ملصق(20261103-152241).txt`
  - `BUGGY_STAGE2_AUTHORITY_DECISION_QUEUE.md` — Buggy Stage 2 authority summary (A-02/A-03/A-04 provenance only)
  - `BUGGY_STAGE2_SOURCE_AUTHORITY_AUDIT.md` — Buggy Stage 2 audit narrative (A-02/A-03/A-04 corroboration only)
  - `PROVENANCE.md` — origin, hashes, and immutability note for all five source files.

## Integrity

- `PACKAGE-MANIFEST.json` lists every package file except the manifest and `SHA256SUMS.txt`.
- `SHA256SUMS.txt` covers every manifest-listed file plus `PACKAGE-MANIFEST.json`; it excludes only itself.
- The three CBH `source-reference/` files are byte-identical to the files in `CBH-METHODOLOGY-PRIMARY-SOURCES.zip`.
- The two Buggy Stage 2 files are byte-identical to the corresponding files in `BUGGY-REFERENCE-HANDOFF-STAGE2-REVISED.zip`; they are included only as provenance for A-02/A-03/A-04 and do not transfer Buggy authority.

## Next action

Run the verification prompt only after extracting this package. Review the resulting report and then make owner decisions on the proposed refinements before calling the baseline approved. Do not start Phase 4, Phase 5, Reference Alignment, migration, or implementation on the basis of this draft.
