# SAMPLING_PROVENANCE — OffsecCyber limited samples

**Dataset:** PentesterFlow/OffsecCyber
**Pinned revision:** `e2aa04114f466659701cf999dfa27a2ebf7054ef`
**Sampling date:** 2026-11-04
**Permitted limits:** Train ≤ 20, Validation ≤ 10, Test ≤ 10 records

---

## 1. Method actually used

### 1.1 HuggingFace dataset viewer — FAILED

The HuggingFace datasets-server rows endpoint was attempted first, with the revision pinned:

```
https://datasets-server.huggingface.co/rows?dataset=PentesterFlow/OffsecCyber&config=default&split=train&offset=0&length=20&revision=e2aa04114f466659701cf999dfa27a2ebf7054ef
```

It returned an error for all three splits:

- `error`: `The dataset generation failed`
- `cause_exception`: `CastError`
- cause: the `messages` field cannot be cast to a single Arrow type because some rows'
  message items carry a `tool_calls` sub-structure and others do not.

**Consequence:** viewer/API row sampling is **not available** for this dataset revision.
The dataset card's own viewer preview is likewise not guaranteed to render.

### 1.2 Bounded HTTP Range reads — USED

Because the viewer is unavailable, samples were retrieved with **HTTP Range requests**
against the pinned revision files, which returns genuine bytes from the requested file
without downloading it:

```
https://huggingface.co/datasets/PentesterFlow/OffsecCyber/resolve/e2aa04114f466659701cf999dfa27a2ebf7054ef/<file>.jsonl
```

| Split | File | Range requested | Complete JSON records parsed | Records retained |
|-------|------|-----------------|------------------------------|------------------|
| train | `train.jsonl` | bytes 0–400,000 | 208 | 20 (first 20) |
| validation | `valid.jsonl` | bytes 0–150,000 | ≥10 | 10 (first 10) |
| test | `test.jsonl` | bytes 0–150,000 | ≥10 | 10 (first 10) |

Only the trailing partial line of each range was discarded; retained records are complete,
valid JSON objects.

**No full dataset was downloaded.** Total bytes read ≈ 700 KB against a ~123 MB dataset.

## 2. Records retained

| File | Lines | Bytes | SHA-256 |
|------|------:|------:|---------|
| `train.jsonl` | 20 | 43,354 | `f184b0f7685debcfc3d304abf26d661af368f9f38fe9996cba3ea7615f1872cb` |
| `validation.jsonl` | 10 | 14,963 | `ec1a3bf0d12a6eac6f1ce24074801efbb56f71393bc12442976f4e99f71563ec` |
| `test.jsonl` | 10 | 23,957 | `17d1dc58ff01c5007116a2b35595b59196f17d0a4b5d1b474619fe765222876e` |

All 40 `metadata.dataset_key` values are unique. No duplicate CVE IDs within any retained
sample.

## 3. `CVE-2023-52357` investigation

The previous sample-quality inventory contained `CVE-2023-52357` **twice** in the Train
section. Verification:

- It does **not** appear in the permitted first-20 Train sample (0 occurrences).
- It **does** appear once further into the scanned 400 KB range, at complete-record index
  **35** (0-based) within that range, source `qwen_cve`, dataset_key
  `00333b1ec99e17ed9f955251f008a137d7b6657827f73182ccba97d7a0ba0b1d`.
- That record lies outside the permitted 20-record sample and is therefore **not** included.

**Conclusion:** the duplicated rows in the old inventory were unsupported. The rebuilt
inventory contains no `CVE-2023-52357` row.

## 4. Important schema observation

The retained samples reveal that **the metadata schema is not uniform across splits**:

- Validation records commonly carry `quality_score`, `completeness`, `cvss_score`,
  `severity`, `missing_sections`, `has_future_cve`, `is_negative`, `is_short_response`,
  `repetitive_prompt`, `rejection_reason`.
- Many Train records carry `source_name`, `source_url`, `source_record_*`, `official_cwe_ids`,
  `fact_scope`, `reference_chunk_*`, `task`, and may **omit** `quality_score`/`completeness`
  (notably NVD-sourced records).
- Test records show a mixture.
- Per-source field sets differ (e.g. HackerOne records carry `id`, `program`,
  `severity_rating`, `is_paraphrased`; offensive-education records carry `chapter`,
  `difficulty`, `domain`, `category`).

This heterogeneity is the same condition that breaks the HuggingFace viewer (CastError on
`messages`). It means the dataset should be treated as a **union of per-source schemas**,
not a single flat table.

## 5. Boundaries respected

- Full dataset **not** downloaded.
- Sample counts within limits (20/10/10).
- No sample identifiers, CVEs, or metadata invented — every row is copied verbatim from the
  pinned revision.
- Raw full clone not included; only the 40 retained records are packaged.
