# SOURCE_METADATA.md — OffsecCyber

## Dataset Identification

| Field | Value | Verification |
|-------|-------|--------------|
| Dataset URL | https://huggingface.co/datasets/PentesterFlow/OffsecCyber | Observed |
| Owner account | PentesterFlow | Observed (HF API) |
| Dataset name | OffsecCyber | Observed |
| Pinned revision | `e2aa04114f466659701cf999dfa27a2ebf7054ef` | Observed (HF API) |
| Pinned commit date | 2026-11-03T20:19:14Z | Observed (commits API) |
| Pinned commit title | "Update dataset card: enhanced build counts, composition, processing pipeline…" | Observed |
| Commits at inspection | 6 | Observed (commits API) |
| Inspection date | 2026-11-04 | — |
| License | Apache 2.0 | `LICENSE` file present (11,358 B) + README front-matter |
| Viewability | HF dataset viewer **broken** (CastError) | Observed |

**This dataset is used at the pinned revision only. No metrics from other revisions are mixed in.**

---

## File Listing (pinned revision)

Sizes obtained from the HuggingFace API (`?blobs=true`), i.e. exact byte sizes at this revision.

| File | Bytes | Approx. | Blob ID (prefix) |
|------|------:|---------|------------------|
| `train.jsonl` | 109,410,121 | 109.4 MB | `511bfad85ba8` |
| `valid.jsonl` | 6,120,122 | 6.12 MB | `03e73cbe5b09` |
| `test.jsonl` | 6,070,883 | 6.07 MB | `9b9e6bfd31c1` |
| `README.md` | 9,868 | 9.87 KB | `63e3742232dd` |
| `manifest.json` | 7,470 | 7.47 KB | `fbd566d00b2d` |
| `LICENSE` | 11,358 | 11.4 KB | `d64569567334` |
| `.gitattributes` | 2,552 | 2.55 KB | `e68665eafbf7` |
| `banner.png` | 1,345,723 | 1.35 MB | `6bd25e21514c` |
| **Sum of files** | **122,978,097** | **≈123 MB** | — |

Note: `usedStorage` reported by the API is 195,718,427 bytes; that figure includes repository/LFS overhead and is **not** the sum of current file sizes. The 123 MB documented size matches the sum of the current blobs.

---

## Metrics reconciliation (pinned revision only)

Every figure below is tied to `e2aa04114f466659701cf999dfa27a2ebf7054ef`.
Legend: **VERIFIED** = corroborated by two or more artifacts at the pinned revision;
**DOCUMENTED_CLAIM** = stated in README/manifest but not independently recounted;
**UNVERIFIED** = unresolved inconsistency or ambiguous definition.

### Splits and totals

| Metric | Value | Artifact(s) | Status |
|--------|------:|-------------|--------|
| Total records | 60,517 | README §Dataset splits; manifest split sum | VERIFIED (arithmetic) |
| Train records | 54,484 | README; `manifest.splits.train.records` | VERIFIED |
| Validation records | 3,017 | README; `manifest.splits.valid.records` | VERIFIED |
| Test records | 3,016 | README; `manifest.splits.test.records` | VERIFIED |
| Split sum check | 54,484 + 3,017 + 3,016 = 60,517 | — | VERIFIED |

Line-level recount of the `.jsonl` files would require downloading ~123 MB; it was **not
performed** under the "do not download the full dataset" constraint. The total is therefore
verified as an *internal arithmetic consistency*, not by line counting.

### Source distribution

| `training_source` | Records | Share | Status |
|-------------------|--------:|------:|--------|
| `qwen_cve` | 30,956 | 51.2% | VERIFIED (README + manifest sum) |
| `NVD CVE 2.0 annual feed` | 21,228 | 35.1% | VERIFIED |
| `web_offensive_elite_v2_sft` | 5,673 | 9.4% | VERIFIED |
| `h1` | 2,350 | 3.9% | VERIFIED |
| `portswigger_labs_sft` | 273 | 0.5% | VERIFIED |
| `gapfill_synthetic` | 21 | <0.1% | VERIFIED (README; present in gapfill_merged) |
| `Official CVE Program record (CVEProject/cvelistV5)` | 16 | <0.1% | VERIFIED |
| **Sum** | **60,517** | **100%** | VERIFIED |

`manifest.splits.*.sources` sums to **60,496**, i.e. it **excludes the 21 `gapfill_synthetic`
records**. `60,496 + 21 = 60,517` — reconciled, not a contradiction.

### Label coverage

| Metric | Value | Derivation | Status |
|--------|------:|------------|--------|
| Labeled records | 57,662 | 51,877 + 2,893 + 2,892 (`manifest.splits.*.labeled`) | VERIFIED |
| Class coverage | 95.3% | 57,662 / 60,517 = 95.28% | VERIFIED |
| Unlabeled records | ~2,834 | 60,496 − 57,662 | VERIFIED but **denominator-sensitive** |
| Unlabeled, alternate basis | 2,855 | 60,517 − 57,662 | Arithmetic alternative |
| Declared class count | 35 | README §Labels | DOCUMENTED_CLAIM |
| Declared CWE map size | 183 | README; `manifest.fixes.cwe_map_size` | VERIFIED |

The ~2,834 figure uses the pre-gapfill denominator (60,496). Using the final total (60,517)
gives 2,855. Both are arithmetically sound; the README does not state which basis it uses.
**Documented as a definitional ambiguity, not a data error.**

### Processing pipeline

| `manifest.fixes` field | Value | README agreement | Status |
|------------------------|------:|------------------|--------|
| `input` | 100,789 | README: 100,789 raw merged records | VERIFIED |
| `after_exact_dedup` | 100,789 | No exact duplicates claimed | VERIFIED |
| `cwe_map_size` | 183 | README: 183 CWEs | VERIFIED |
| `dropped_future` | 3,899 | README: 3,899 `has_future_cve` rows dropped | VERIFIED |
| `class_backfilled` | 58,524 | README: coverage 37% → 95.3% | **UNVERIFIED** |
| `sysprompt_rotated` | 42,997 | README: top-prompt share 57% → ~9% | DOCUMENTED_CLAIM (not recomputable) |
| `overflow_isolated` | 257 | README: 257 over-length rows held out | VERIFIED |
| `near_dup_templates_capped` | 36,137 | README: 36,137 near-duplicates removed | VERIFIED |
| `after_all_fixes` | 60,496 | README: 60,517 final | **Reconciled via gapfill** |

**`class_backfilled = 58,524` is inconsistent with the README narrative** if interpreted as
"number of rows whose class was backfilled": with 57,662 labeled rows in the final build and
~37% pre-existing coverage, the implied backfill count is ~35,000, not 58,524. The field may
count pre-dedup operations or boolean-flag occurrences over the raw 100,789 rows
(58,524 / 100,789 = 58.1%). Its exact definition is **not specified**. Marked **UNVERIFIED**.

**`after_all_fixes = 60,496`** is the pre-gapfill total; `60,496 + 21 = 60,517`. Reconciled.

### Class taxonomy discrepancy

| Item | Value | Status |
|------|------:|--------|
| README declared vulnerability/report classes | 35 | DOCUMENTED_CLAIM |
| `manifest.json:classes` array length | 219 | VERIFIED (parsed) |
| Nature of `manifest.classes` | Mixed topic/chapter strings | OBSERVED |

`manifest.json:classes` is **not** the 35-label `metadata.class` vocabulary. It is a mixed
list containing course/chapter names (e.g. `"API Breaches & Bug Bounties"`,
`"Android Application Security"`) alongside label-like strings (`"xss"`, `"xxe"`, `"web"`).
**Do not equate the two.** The 35-label set is described only in README §Labels.

Additionally, README §Labels says to "consult `manifest.json` for exact counts by split",
but `manifest.splits.*` contains only `records`, `sources`, and `labeled` — **no per-class
counts**. That README statement is **not supported** by the manifest at this revision.
Marked **DISCREPANCY (documentation)**.

### Other metrics

| Metric | Value | Status |
|--------|------:|--------|
| Total commits | 6 | VERIFIED (commits API) |
| Contributors | 1 account visible (`PentesterFlow`) | PARTIAL — individual commit authors not enumerated |
| Dataset size category | 10K < n < 100K | VERIFIED (card metadata) |
| Declared memory-safety share | ~0.7% | DOCUMENTED_CLAIM (not recounted) |
| Declared answers-with-code share | ~3% | DOCUMENTED_CLAIM (not recounted) |
| Declared cross-split CVE leakage | 0 | DOCUMENTED_CLAIM (not re-audited) |

---

## Inspection method

1. HF API metadata at the pinned revision (`/api/datasets/.../revision/<sha>?blobs=true`).
2. README.md and manifest.json fetched from the pinned revision URL.
3. Dataset viewer (`datasets-server.huggingface.co/rows`) attempted — **failed** with
   `CastError` on `messages` (heterogeneous `tool_calls` shape).
4. Samples obtained via **bounded HTTP Range requests** against the pinned revision files
   (≈700 KB total, not the full dataset). See
   `limited-samples/SAMPLING_PROVENANCE.md`.
5. No full dataset download. No training or execution.

---

## Schema summary (observed)

The dataset is a **union of per-source schemas**, not a single flat table. Fields commonly
present include `messages[]`, `metadata.dataset_key`, `metadata.split`,
`metadata.merged_collection`, `metadata.merged_from_split`, `metadata.training_source`,
`metadata.class`, `metadata.cve_ids`, `metadata.cwe`, `metadata.cvss_score`,
`metadata.severity`, `metadata.quality_score`, `metadata.completeness`, and various flags.

- Validation records frequently carry quality/completeness fields.
- Many Train records (especially NVD-sourced) **omit** `quality_score`/`completeness`.
- HackerOne records carry `id`, `program`, `severity_rating`, `is_paraphrased`.
- Offensive-education records carry `chapter`, `difficulty`, `domain`, `category`.
- `messages[].tool_calls` and top-level `tools` are documented but were **absent from all 40
  retained samples**.

Full field list: `inventories/OFFSECCYBER_SCHEMA.csv`.

---

## Limitations

1. Viewer unavailable — no reproducible viewer links.
2. Total record count is internally consistent but **not line-recounted** (no full download).
3. `class_backfilled` definition unresolved → UNVERIFIED.
4. `manifest.classes` ≠ 35-class label vocabulary → documented discrepancy.
5. Per-class counts are not present in the manifest despite the README implying they are.
6. Dataset is annotated, not authoritative; values must be verified against primary sources.
7. Apache 2.0 covers the dataset compilation; **third-party content provenance is not
   established** by the licence.
