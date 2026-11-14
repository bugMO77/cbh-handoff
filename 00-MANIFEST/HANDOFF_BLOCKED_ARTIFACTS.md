# BLOCKED_ARTIFACTS — reasons only, no sensitive values

This register documents artifacts that were **not** included in the handoff package.
Only reasons are recorded; no secret values, contents, or private data are reproduced.

---

## 1. AI-HUNTING source snapshot (154 curated files)

- Reason: creator permission context is UNVERIFIED for redistribution; no LICENSE file
  exists in the upstream repository (`0xmannaf/Ai-Hunting`); snapshot is preserved for
  private internal study only.
- Decision: include METADATA only in this handoff package (see `04-AI-HUNTING/`).
- Local original preserved at:
  `/home/kali/cbh-reference-intake/external-sources/ai-hunting/source-snapshot/`
  and `/home/kali/CBH-WORKSPACE/03_EXTERNAL_REFERENCES/AI-HUNTING/SNAPSHOT/`.
- Owner decision requested on 2026-11-14: metadata-only. (Owner answered metadata-only.)

## 2. OffsecCyber sample records (40 rows: 20 train / 10 valid / 10 test)

- Reason: license declared Apache-2.0 on the dataset card, but third-party content rights
  are UNRESOLVED; redistribution is NOT CLEARED.
- Decision: include metadata + review reports + provenance only (see `05-SOURCES/`).
  The records themselves stay local at
  `/home/kali/cbh-reference-intake/external-sources/offseccyber/limited-samples/`.
- Owner decision requested on 2026-11-14: metadata-only. (Owner answered metadata-only.)

## 3. Local machine material (never part of any upload)

- `~/.ssh/`, `~/.mozilla/`, `~/.BurpSuite/`, `~/.gnupg/`, `~/.hermes/`,
  `~/.zsh_history`, `~/.gitconfig`, `~/.config/` — private machine/browser/session data.
- `~/tools/Cybermes-source-backup-20261029-034845.tar.gz` (~357 MB) — backup of an
  unrelated source tree (`Cybermes`); not part of CBH / BUGGY; local only.
- `~/Downloads/` chat-export packages — local reference archives; not part of this package.
- `~/my tools or scripts/`, `~/some py files/`, `~/minimax-dahl/` — local tooling &
  scratch; not part of this package.

## 4. CBH validation results

- None exist. No fabricated results were created. See `07-VALIDATION/`.

## 5. cbh-handoff repository (GitHub)

- NOT CREATED (owner decision: local-only in this phase). Recorded as MISSING.

---

## Security gate summary

| Artifact | CONTAINS_SECRETS | PRIVATE/PERSONAL | SAFE_LOCALLY | PUBLIC_SAFE | Status |
|---|---|---|---|---|---|
| AI-HUNTING curated snapshot | NO (curation scan) | NO | YES | NO | BLOCKED from upload (permission not cleared) |
| OffsecCyber 40 records | NO (bounded sample) | YES — real target-derived content | YES | NO | BLOCKED from upload (third-party rights unresolved) |
| Cybermes backup tarball | UNKNOWN | YES | YES | NO | BLOCKED from upload (unrelated local backup) |
| ~/.ssh, browser & session data | YES (likely) | YES | YES | NO | BLOCKED from upload |
| tool-installation-report.json | NO | YES (local paths) | YES | NO | IN PACKAGE but private-only (02-BUGGY) |
