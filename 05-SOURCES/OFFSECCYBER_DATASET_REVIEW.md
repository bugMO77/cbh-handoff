# OFFSECCYBER_DATASET_REVIEW

**Dataset:** PentesterFlow/OffsecCyber
**HuggingFace URL:** https://huggingface.co/datasets/PentesterFlow/OffsecCyber
**Pinned revision:** `e2aa04114f466659701cf999dfa27a2ebf7054ef`
**Revision date:** 2026-11-03T20:19:14Z
**Inspection date:** 2026-11-04
**License:** Apache 2.0 (`LICENSE` present, 11,358 bytes)

> All figures below refer to the pinned revision only. No figures from earlier revisions
> are mixed in. Where a figure could not be resolved it is marked **UNVERIFIED** rather
> than rounded to a convenient value.

---

## 1. Source identity

| Field | Value | Basis |
|-------|-------|-------|
| Owner | PentesterFlow | HF API |
| Dataset | OffsecCyber | HF API |
| Task categories | text-generation, text-classification | Card metadata |
| Language | en | Card metadata |
| Size category | 10K < n < 100K | Card metadata |
| License | apache-2.0 | `LICENSE` + README front-matter |
| Commits | 6 | Commits API |
| Reported storage | 195,718,427 B (repo overhead included) | HF API |
| Sum of current files | 122,978,097 B (≈123 MB) | HF API blob sizes |

The 123 MB figure in the dataset card is the sum of the current file blobs, not the
`usedStorage` value (which includes repository/LFS overhead).

### 1.1 Files

| File | Bytes | Role |
|------|------:|------|
| `train.jsonl` | 109,410,121 | Train split |
| `valid.jsonl` | 6,120,122 | Validation split (split name is `validation`) |
| `test.jsonl` | 6,070,883 | Test split |
| `README.md` | 9,868 | Dataset card |
| `manifest.json` | 7,470 | Processing manifest |
| `LICENSE` | 11,358 | Apache 2.0 text |
| `.gitattributes` | 2,552 | Git LFS attributes |
| `banner.png` | 1,345,723 | Banner image |

---

## 2. Splits and source composition

| Split | Records |
|-------|--------:|
| Train | 54,484 |
| Validation | 3,017 |
| Test | 3,016 |
| **Total** | **60,517** |

`54,484 + 3,017 + 3,016 = 60,517` — internally consistent (README and
`manifest.splits` agree). **Not line-recounted**, because that requires downloading the
full ~123 MB, which is out of scope.

| `training_source` | Records | Share |
|-------------------|--------:|------:|
| `qwen_cve` (synthetic CVE analysis) | 30,956 | 51.2% |
| `NVD CVE 2.0 annual feed` | 21,228 | 35.1% |
| `web_offensive_elite_v2_sft` | 5,673 | 9.4% |
| `h1` (HackerOne) | 2,350 | 3.9% |
| `portswigger_labs_sft` | 273 | 0.5% |
| `gapfill_synthetic` | 21 | <0.1% |
| `Official CVE Program record` | 16 | <0.1% |
| **Total** | **60,517** | **100%** |

`manifest.splits.*.sources` sums to 60,496, excluding the 21 `gapfill_synthetic` records.
`60,496 + 21 = 60,517` — reconciled.

Synthetic content is therefore **30,977 records (51.2%)** (`qwen_cve` + `gapfill_synthetic`).

---

## 3. Schema — union of per-source schemas

### 3.1 Top level

Each JSONL line is an object with `messages` (required) and `metadata` (required).
A small number of documented records additionally carry top-level `tools`.

### 3.2 `messages`

- Array of message objects.
- Observed item keys: `role`, `content`.
- Documented optional item key: `tool_calls` (on assistant turns of tool-calling records).
- Observed roles: `system`, `user`, `assistant` (README also lists occasional `tool`).
- Observed message counts in the 40 samples: 3 (dominant), 9, 11.
- **No `tool_calls` occurred in any of the 40 retained samples.**

### 3.3 `metadata` heterogeneity — a key finding

The metadata field set is **not uniform across splits or sources**:

| Population | Typical metadata fields |
|------------|-------------------------|
| Validation records | `quality_score`, `completeness`, `cvss_score`, `severity`, `missing_sections`, `has_future_cve`, `is_negative`, `is_short_response`, `repetitive_prompt`, `rejection_reason`, `num_turns`, `response_length` |
| Train NVD records | `source_name`, `source_url`, `source_record_published`, `source_record_last_modified`, `source_record_status`, `official_cwe_ids`, `fact_scope`, `task`; often **no** `quality_score`/`completeness` |
| Train `qwen_cve` records | `quality_score`, `completeness`, `cvss_score`, `severity`, `class_backfilled` |
| HackerOne (`h1`) | `id`, `program`, `severity_rating`, `is_paraphrased`, `quality_score` |
| `web_offensive_elite_v2_sft` | `chapter`, `difficulty`, `domain`, `category`, `section`, `file`, `source`, `source_author`, `license`, `source_repo` |

Consequences:

- The dataset must be treated as a **union of per-source schemas**, not a flat table.
- Field presence is source-dependent; absent fields are not necessarily missing data errors.
- The heterogeneity is the likely cause of the HuggingFace **viewer CastError** (see §5).

Full observed field list with presence counts: `inventories/OFFSECCYBER_SCHEMA.csv`.

### 3.4 Observed value types (40-sample basis)

| Field | Observed types | Present |
|-------|----------------|--------:|
| `metadata.dataset_key` | string | 40/40 |
| `metadata.training_source` | string | 40/40 |
| `metadata.split` | string | 40/40 |
| `metadata.class` | string | 39/40 |
| `metadata.cve_ids` | array | 36/40 |
| `metadata.cwe` | string | 28/40 |
| `metadata.cvss_score` | float \| null | 24/40 |
| `metadata.quality_score` | integer | 26/40 |
| `metadata.completeness` | float | 24/40 |
| `metadata.severity` | string | 24/40 |
| `metadata.missing_sections` | array | 24/40 |
| `metadata.has_future_cve` | boolean | 24/40 |
| `metadata.is_negative` | boolean | 26/40 |
| `metadata.class_backfilled` | boolean | 13/40 |
| `metadata.num_turns` | integer | 26/40 |

---

## 4. Labels

- README declares **35 vulnerability/report classes**.
- Declared largest classes: `xss` 8,290; `cmdi` 7,243; `access_control` 6,758;
  `info_disclosure` 6,232; `auth` 5,820; `pathtraver` 4,967.
- `manifest.json` labeled counts: 51,877 (train) + 2,893 (valid) + 2,892 (test) = **57,662**
  → **95.3% coverage** of 60,517.
- Unlabeled: **~2,834** using the pre-gapfill denominator (60,496); **2,855** using 60,517.
  The README does not state the basis — a definitional ambiguity, not a data error.
- `manifest.fixes.cwe_map_size` = 183 CWEs, matching README.

### 4.1 Taxonomy discrepancy — `manifest.classes`

`manifest.json:classes` contains **219** entries. It is **not** the 35-label
`metadata.class` vocabulary. It mixes course/chapter titles (`"API Breaches & Bug Bounties"`,
`"Android Application Security"`) with label-like strings (`"xss"`, `"xxe"`, `"web"`).
Equating `len(manifest.classes)` with "35 classes" is incorrect.

Additionally, README §Labels says to consult `manifest.json` for per-split class counts, but
`manifest.splits.*` contains only `records`, `sources`, and `labeled`. **No per-class counts
exist in the manifest at this revision.** This is a documentation discrepancy.

---

## 5. Sampling method and the viewer failure

### 5.1 Viewer failure (observed)

The HuggingFace datasets-server rows endpoint was called with the revision pinned:

```
/datasets-server/rows?dataset=PentesterFlow/OffsecCyber&config=default&split=<split>&offset=0&length=<n>&revision=e2aa041...
```

All three splits returned:

- `error`: `The dataset generation failed`
- `cause_exception`: `CastError`
- cause: the `messages` field cannot be cast to one Arrow type because some message items
  carry a `tool_calls` sub-structure and others do not.

**Therefore the dataset viewer is not usable for this revision**, and earlier claims of
"sampled via the viewer" were not reproducible. Viewer-generated preview links cannot be
provided.

### 5.2 Method actually used

Bounded **HTTP Range** requests against the pinned revision files:

| Split | File | Range | Complete records parsed | Retained |
|-------|------|-------|------------------------:|---------:|
| Train | `train.jsonl` | 0–400,000 B | 208 | 20 |
| Validation | `valid.jsonl` | 0–150,000 B | ≥10 | 10 |
| Test | `test.jsonl` | 0–150,000 B | ≥10 | 10 |

≈700 KB read out of ~123 MB. **No full download.** Records retained verbatim; no fields
invented. Provenance: `external-sources/offseccyber/limited-samples/SAMPLING_PROVENANCE.md`.

---

## 6. `CVE-2023-52357` duplicate investigation

The earlier sample-quality inventory listed `CVE-2023-52357` **twice** under Train.

Findings:

- It is **not** in the permitted first-20 Train sample (0 occurrences).
- It occurs **once** at complete-record index 35 within the scanned 400 KB range
  (`training_source = qwen_cve`, dataset_key
  `00333b1ec99e17ed9f955251f008a137d7b6657827f73182ccba97d7a0ba0b1d`).
- That record is outside the permitted sample window and is not included.

**Conclusion:** the duplicated rows were unsupported. The rebuilt
`inventories/OFFSECCYBER_SAMPLE_QUALITY.csv` contains **0** rows for this CVE and exactly
**20 Train / 10 Validation / 10 Test** records, all with unique `dataset_key` values.

---

## 7. Processing pipeline figures (pinned revision)

| Field | Value | Status |
|-------|------:|--------|
| Raw merged input | 100,789 | VERIFIED |
| Exact dedup | 100,789 (no exact duplicates) | VERIFIED |
| CWE map size | 183 | VERIFIED |
| Forward-dated CVE rows dropped | 3,899 | VERIFIED |
| Near-duplicate templates capped | 36,137 | VERIFIED |
| Over-length rows held out | 257 | VERIFIED |
| Gap-fill added | 21 (reasoning 15, tool 6) | VERIFIED |
| After all fixes | 60,496 | VERIFIED (pre-gapfill) |
| Final total | 60,517 | VERIFIED (60,496 + 21) |
| `class_backfilled` | 58,524 | **UNVERIFIED** (definition unclear; see §8) |
| `sysprompt_rotated` | 42,997 | DOCUMENTED_CLAIM |
| `tool_total` (coverage block) | 48 | **UNVERIFIED** (unit unclear; gapfill tool shapes = 6) |

---

## 8. Unresolved / UNVERIFIED items

1. **`class_backfilled = 58,524`** cannot be a simple count of backfilled final rows:
   with 57,662 labeled rows and ~37% pre-existing coverage, the implied backfill is
   ~35,000. It may be computed pre-dedup or as a flag across raw rows. Definition
   unspecified → **UNVERIFIED**.
2. **`manifest.classes` (219) vs 35 declared classes** → not the same taxonomy; resolved as
   a documentation ambiguity, but the actual per-class counts remain unavailable in the
   manifest.
3. **No line-level recount** of splits — total is verified by arithmetic only.
4. **`tool_total = 48`** unit undefined (records? turns? messages?) → **UNVERIFIED**.
5. **Third-party content provenance** is not established by the Apache 2.0 licence.
6. **Declared shares** (memory-safety ~0.7%, code ~3%, cross-split leakage 0) are
   documented claims, not re-audited.

---

## 9. Data quality notes (evidence-based)

- 51.2% synthetic (`qwen_cve`); the dataset card itself cautions that `cvss_score`,
  `severity`, and `class` are annotations, not authoritative ratings.
- Some records have `cve_ids` containing forward-dated years (e.g. a 2026 CVE appeared in
  the validation sample). The README claims forward-dated rows were filtered; the fields
  `has_future_cve` and `cvss_score_status` remain on some rows. Whether those retained
  records are genuinely valid or survivors of a partial filter is **UNVERIFIED**.
- One observed Train record had `class = null` and no CVE (offensive-education source), so
  unlabeled rows are not confined to a single source.
- Quality/completeness scores exist mainly on `qwen_cve` and validation records; NVD records
  generally lack them. Quality metrics are therefore **not comparable across sources**.

---

*Reviewed source: https://huggingface.co/datasets/PentesterFlow/OffsecCyber @ `e2aa041`*
