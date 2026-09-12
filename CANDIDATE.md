# Candidate Freeze Submission: battery-deposit-semantics-s1 (Final Terminal Remediation)

## 1. Candidate Overview
- **Instance:** `battery-deposit-semantics-s1`
- **Submission Type:** Pre-Execution Preregistration Freeze Package (Addressing G-1 through G-5)
- **Governing Protocol:** P10 Strict Boundary Specification

---

## 2. Gate Finding Remediation Log (Terminal Round)

| Finding | Remediation Action & Implementation | Primary Artifact |
|---|---|---|
| **G-1** | Resolved contradiction between Preregistration and Instrument. Explicitly recognized that `CALIBRATION_POSITIVE` (Chung 2021) is a non-blind internal consistency test; instance disclaims blind-falsifiability. Decoupled `CONFIRMATORY_HIGH_DOC_CONTROL` as an empirical test where non-resolution does not invalidate the instrument. Purged legacy `CONFIRMATORY_POSITIVE` terminology. | [`PREREGISTRATION.md`](PREREGISTRATION.md), [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md) |
| **G-2** | Pinned deterministic High-Doc candidate pool prior to freeze. Retrieved and frozen literal Crossref response (`scientific_data_crossref_raw.json`), extracted candidate list using objective criteria, pinned ISSN `2052-4463`, and eliminated post-freeze moving denominators. | [`scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json), `artifacts/sampling_frame/` |
| **G-3** | Clarified canonical Table-2 source unambiguously: bibliographic work is dos Reis et al. 2021 (DOI: `10.1016/j.egyai.2021.100081`); canonical S1 sampling artifact is the pinned accepted-manuscript PDF (`dos_reis_2021_accepted_manuscript.pdf`), Table 2, page 12. | [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md) §1 |
| **G-4** | Replaced naive substring keyword filter with complete, explicit, item-by-item domain adjudication of all 36 Crossref records in `scientific_data_eligibility.tsv`. Isolated exactly 7 `IN_SCOPE` rechargeable lithium-ion cycling datasets, discarding zinc-oxygen/air, bicycle, and recycling datasets. Re-ranked candidate pool places lithium-ion characterization dataset `10.1038/s41597-025-05725-y` at Rank 1. Documented candidate pool exposure in `PRE_FREEZE_EXPOSURE.md` and `FAILURES.md`. | [`scientific_data_eligibility.tsv`](artifacts/sampling_frame/scientific_data_eligibility.tsv), [`FAILURES.md`](FAILURES.md) |
| **G-5** | Recomputed and synchronized all artifact checksums mechanically. Generated single authoritative checksum inventory in [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS), eliminating stale declared hash references. | [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS) |
| **Uniform Correspondence** | Confirmed and reinforced the Uniform Correspondence Protocol across all confirmatory datasets (1 High-Doc Control + 2 Targets) with a 14-calendar-day window and two-dimensional output. | [`INSTRUMENT.md`](INSTRUMENT.md) §4, [`PREREGISTRATION.md`](PREREGISTRATION.md) §2 |

---

## 3. Pinned Artifact Inventory & Authoritative Checksums

All checksums below are mechanically synchronized with [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS):

```text
3c3b55e217fa2925a970c69505acd943ff945b0f4a64dac002a4ec691b5648fb  dos_reis_2021_accepted_manuscript.pdf
c81654c225c51d43bc4de3a9d373c0b217c66b2d3752e39de5606e35c7fe7736  dos_reis_2021_table2.tsv
854f7da7770d68a564b31a2b242d22d103b31b205c928bb13c84225c3ee8c83f  scientific_data_crossref_raw.json
c2d9daf3cb12a140b5ca159566708326a5434eb79802da055aff9796971f867f  scientific_data_eligibility.tsv
e75fed70f0c88e37525c90d1be03c899a6e7da58be3e42d0ebb11e2e1d44bd32  scientific_data_candidates.tsv
f6c3b44691555fcf0ee9c1282259c7b3cee7981749ede239febfacc038925ef7  scientific_data_pool_spec.json
```

1. **Measurement Instrument:** [`INSTRUMENT.md`](INSTRUMENT.md)
2. **Sampling Protocol & Denominator:** [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md)
3. **Epistemic Disclosures:** [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md)
4. **Execution Invariants & State:** [`PREREGISTRATION.md`](PREREGISTRATION.md) & [`STATUS.md`](STATUS.md)

---

## 4. Execution Invariants Maintained
- Zero target deposit repository URLs opened pre-freeze (`target_deposit_inspections_pre_freeze: 0`).
- Target repository contents of candidate `10.1038/s41597-025-05725-y` strictly unopened.
- Execution state HALT.
