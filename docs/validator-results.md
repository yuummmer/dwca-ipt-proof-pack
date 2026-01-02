# Validator Results

This file records validation runs for the DwC-A exports and fixtures in this repo.

## Validator used
- GBIF Data Validator (web UI)
- Date run: 2026-01-02
- Notes: Screenshots (optional) can be saved under `docs/screenshots/`.

---

## Summary

| Artifact | Path | Expected | Observed | Key message / error |
|---|---|---:|---:|---|
| Baseline export | `dwca/dwca-occ-proofpack-v1.0.zip` | PASS | TODO | TODO |
| Good fixture | `fixtures/zips/good.zip` | PASS | TODO | TODO |
| Broken 1: duplicate IDs | `fixtures/zips/broken-1-duplicate-ids.zip` | FAIL | TODO | TODO |
| Broken 2: missing scientificName | `fixtures/zips/broken-2-missing-scientificName.zip` | FAIL | TODO | TODO |
| Broken 3: bad meta.xml reference | `fixtures/zips/broken-3-bad-meta.zip` | FAIL | TODO | TODO |

---

## Details

### 1) Baseline export: `dwca/dwca-occ-proofpack-v1.0.zip`
- Observed: TODO
- Notes: TODO

### 2) Good fixture: `fixtures/zips/good.zip`
- Observed: TODO
- Notes: TODO

### 3) Broken 1 (duplicate core IDs): `fixtures/zips/broken-1-duplicate-ids.zip`
- Expected failure reason:
  - Duplicate DwC-A core IDs (core ID defined in `meta.xml` as `<id index="0" />`)
- Observed: TODO
- Notes: TODO

### 4) Broken 2 (missing `scientificName`): `fixtures/zips/broken-2-missing-scientificName.zip`
- Expected failure reason:
  - Required term missing / schema mismatch (removed `scientificName` column from `occurrence.txt` without updating `meta.xml`)
- Observed: TODO
- Notes: TODO

### 5) Broken 3 (bad `meta.xml` file reference): `fixtures/zips/broken-3-bad-meta.zip`
- Expected failure reason:
  - `meta.xml` references a core file that doesn’t exist (renamed `occurrence.txt`)
- Observed: TODO
- Notes: TODO
