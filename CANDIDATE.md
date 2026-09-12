# Candidate Freeze Submission: battery-deposit-semantics-s1 (Sealed Pre-Execution State)

## 1. Candidate Overview
- **Instance:** `battery-deposit-semantics-s1`
- **Submission Type:** Pre-Execution Preregistration Freeze Package (Sealed & Verified)
- **Governing Protocol:** P10 Strict Boundary Specification

---

## 2. Gate Finding Remediation Summary

| Finding | Remediation Action & Implementation | Primary Artifact |
|---|---|---|
| **G-1** | Resolved contradiction between Preregistration and Instrument. Explicitly recognized that `CALIBRATION_POSITIVE` (Chung 2021) is a non-blind internal consistency test; instance disclaims blind-falsifiability. Decoupled `CONFIRMATORY_HIGH_DOC_CONTROL` as an empirical test where non-resolution does not invalidate the instrument. Purged legacy `CONFIRMATORY_POSITIVE` terminology. | [`PREREGISTRATION.md`](PREREGISTRATION.md), [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md) |
| **G-2 & G-4** | Pinned deterministic High-Doc candidate pool prior to freeze. Retrieved and frozen literal Crossref response (`scientific_data_crossref_raw.json`), extracted and classified all 36 items in `scientific_data_eligibility.tsv`. Demoted titles lacking proof of both chemistry and regime to `INSUFFICIENT_METADATA_TO_CLASSIFY`. The 3 verified `IN_SCOPE` items ranked deterministically; Rank 1 is `10.1038/s41597-024-03831-x`. | [`scientific_data_eligibility.tsv`](artifacts/sampling_frame/scientific_data_eligibility.tsv), [`scientific_data_candidates.tsv`](artifacts/sampling_frame/scientific_data_candidates.tsv) |
| **G-3** | Clarified canonical Table-2 source unambiguously: bibliographic work is dos Reis et al. 2021 (DOI: `10.1016/j.egyai.2021.100081`); canonical S1 sampling artifact is the pinned accepted-manuscript PDF (`dos_reis_2021_accepted_manuscript.pdf`), Table 2, page 12. | [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md) §1 |
| **G-5** | Recomputed and synchronized all artifact checksums mechanically. Generated single authoritative checksum inventory in [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS). | [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS) |
| **N-1** | Resolved target deposit observation-unit collapse. Formalized observation unit as unique canonical deposit location (`lower(strip(Location with weblink))`). Instituted sampling without replacement at observation-unit level: Rank 1 selected (`TRI [71, URL]` / `[72]`), Rank 2 skipped as `SAME_DEPOSIT_LOCATION_DUPLICATE`, and Rank 3 selected (`KIT [86, URL]` / `[8]`). | [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md) §3.C, [`FAILURES.md`](FAILURES.md) F-004 |
| **N-2** | Realigned High-Doc candidate domain scope to strictly require cycling/aging/degradation of rechargeable lithium-ion cells or packs. Demoted cathode material study (`10.1038/s41597-022-01217-5`) to `OUT_OF_SCOPE`. Candidate Rank 1 invariant (`10.1038/s41597-024-03831-x`). | [`scientific_data_eligibility.tsv`](artifacts/sampling_frame/scientific_data_eligibility.tsv), [`scientific_data_candidates.tsv`](artifacts/sampling_frame/scientific_data_candidates.tsv), [`scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json) |
| **Uniform Correspondence** | Confirmed and reinforced the Uniform Correspondence Protocol across all confirmatory datasets (1 High-Doc Control + 2 Targets) with a 14-calendar-day window and two-dimensional output. | [`INSTRUMENT.md`](INSTRUMENT.md) §4, [`PREREGISTRATION.md`](PREREGISTRATION.md) §2 |

---

## 3. Pinned Artifact Inventory & Authoritative Checksums

All checksums below are mechanically synchronized with [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS):

```text
3c3b55e217fa2925a970c69505acd943ff945b0f4a64dac002a4ec691b5648fb  dos_reis_2021_accepted_manuscript.pdf
c81654c225c51d43bc4de3a9d373c0b217c66b2d3752e39de5606e35c7fe7736  dos_reis_2021_table2.tsv
854f7da7770d68a564b31a2b242d22d103b31b205c928bb13c84225c3ee8c83f  scientific_data_crossref_raw.json
eff8cd7907b0f8a26ac1993eb14e716872cfa6005dcca388bac0f886064d2c3f  scientific_data_eligibility.tsv
8758c3a5010493258619b1bd8e091ad58cebe119f058a8e93a4a243e87b9006c  scientific_data_candidates.tsv
7897029254df845e7572dd2ea2a0b7a2454339ce95165f0dc2a7a0f0779d3e98  scientific_data_pool_spec.json
```

1. **Measurement Instrument:** [`INSTRUMENT.md`](INSTRUMENT.md)
2. **Sampling Protocol & Denominator:** [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md)
3. **Epistemic Disclosures:** [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md)
4. **Execution Invariants & State:** [`PREREGISTRATION.md`](PREREGISTRATION.md) & [`STATUS.md`](STATUS.md)

---

## 4. Execution Invariants Maintained
- Zero target deposit repository URLs opened pre-freeze (`target_deposit_inspections_pre_freeze: 0`).
- Target repository contents of candidate `10.1038/s41597-024-03831-x` strictly unopened.
- Execution state HALT.
