# DwC-A / IPT Proof Pack (GBIF)

This repo is a small, reproducible “proof pack” showing how to publish a dataset via **GBIF IPT locally (Docker)**,
export a **Darwin Core Archive (DwC-A)**, validate it, and iterate on common pitfalls.

## Repo layout
- `data/` — source CSV used to create the IPT resource
- `dwca/` — exported DwC-A zip(s) from IPT
- `fixtures/` — good + broken variants (folders + zipped copies)
- `docs/` — notes, screenshots, optional screencast link

## Quickstart

### Run IPT locally (Docker)
From the repo root:

```bash
mkdir -p ipt-data
docker run -d --name gbif-ipt \
  -p 8080:8080 \
  -v "$PWD/ipt-data:/srv/ipt" \
  gbif/ipt
```

Open IPT in your browser:
`http://localhost:8080`

To stop/start later:
```bash
docker stop gbif-ipt
docker start gbif-ipt
```

### Publish + export DwC-A (IPT UI)
In IPT:
1. Create an Occurrence resource (e.g. `occ-proofpack`)
2. Import `data/occurrence.csv` as Source Data
3. Create Darwin Core Mappings and ensure core ID is set (DwC-A exports commonly use an `id` column as the core identifier)
4. Go to Publication -> Publish
5. Download the DwC-A zip and store it in `dwca/`

This repo includes an exported example: `dwca/dwca-occ-proofpack-v1.0.zip`

### Validate + fix loop
Validate the DwC-A using the GBIF Data Validator (web UI) or any DwC-A validator you choose.

Recommended validation targets:
- `dwca/dwca-occ-proofpack-v1.0.zip` (baseline export)
- `fixtures/zips/good.zip` (expected PASS)
- each `fixtures/zips/broken-*.zip` (expected FAIL for the documented reason)

## Fixtures

### Ready-to-validate zips
- `fixtures/zips/good.zip` (expected PASS)
- `fixtures/zips/broken-1-duplicate-ids.zip` - expected:FAIL (duplicate DwC-A core IDs; meta.xml uses `<id index="0" />`)
- `fixtures/zips/broken-2-missing-scientificName.zip` - expected:FAIL (required term missing `scientificName` removed from `occurrence.txt`)
- `fixtures/zips/broken-3-bad-meta.zip` - expected:FAIL (archive descriptor error; `meta.xml` references `occurrence.txt` but the file was renamed)

### Folder versions (for inspection)
- `fixtures/good/`
- `fixtures/broken-1-duplicate-ids/`
- `fixtures/broken-2-missing-scientificName`
- `fixtures/broken-3-bad-meta`

## Common pitfalls (what the broken fixtures demonstrate)
1. Duplicate core IDs: core identifier must be unique accross records
2. Missing required terms / mapping mismatch: required terms like `scientificName` must exist and align with `meta.xml`
3. Broken `meta.xml` file references: filenames in the archive must match what `meta.xml` declares

## Provenance & licensing
- Original content (docs/scripts/synthetic data): CC0 1.0
- Third-party sources (if any): listed in `NOTICE.md`
