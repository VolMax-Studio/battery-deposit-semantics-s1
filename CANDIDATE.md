# Candidate Freeze Submission: battery-deposit-semantics-s1 (Round 2 Remediation)

## 1. Candidate Overview
- **Instance:** `battery-deposit-semantics-s1`
- **Submission Type:** Pre-Execution Preregistration Freeze Package (Addressing G-1, G-2, G-3)
- **Governing Protocol:** P10 Strict Boundary Specification

---

## 2. Gate Finding Remediation Log (Round 2)

| Finding | Remediation Action & Implementation | Primary Artifact |
|---|---|---|
| **G-1** | Resolved contradiction between Preregistration and Instrument. Explicitly recognized that `CALIBRATION_POSITIVE` (Chung 2021) is a non-blind internal consistency test; instance disclaims blind-falsifiability. Decoupled `CONFIRMATORY_HIGH_DOC_CONTROL` as an empirical test where non-resolution does not invalidate the instrument. Purged legacy `CONFIRMATORY_POSITIVE` terminology. | [`PREREGISTRATION.md`](PREREGISTRATION.md), [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md) |
| **G-2** | Pinned deterministic High-Doc candidate pool prior to freeze. Retrieved and frozen literal Crossref response (`scientific_data_crossref_raw.json`), extracted candidate list using objective mechanical title keywords (`scientific_data_candidates.tsv`), pinned ISSN `2052-4463`, and eliminated post-freeze moving denominators. | [`scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json), `artifacts/sampling_frame/` |
| **G-3** | Clarified canonical Table-2 source unambiguously: bibliographic work is dos Reis et al. 2021 (DOI: `10.1016/j.egyai.2021.100081`); canonical S1 sampling artifact is the pinned accepted-manuscript PDF (`dos_reis_2021_accepted_manuscript.pdf`, SHA-256 `3c3b55e2...`), Table 2, page 12. | [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md) §1 |
| **Uniform Correspondence** | Confirmed and reinforced the Uniform Correspondence Protocol across all confirmatory datasets (1 High-Doc Control + 2 Targets) with a 14-calendar-day window and two-dimensional output. | [`INSTRUMENT.md`](INSTRUMENT.md) §4, [`PREREGISTRATION.md`](PREREGISTRATION.md) §2 |

---

## 3. Pinned Artifact Inventory & Verified SHA-256 Checksums

1. **Measurement Instrument:** [`INSTRUMENT.md`](INSTRUMENT.md)
2. **Sampling Protocol & Denominator:** [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md)
3. **Canonical Sampling Artifacts:**
   - Manuscript PDF: [`artifacts/sampling_frame/dos_reis_2021_accepted_manuscript.pdf`](artifacts/sampling_frame/dos_reis_2021_accepted_manuscript.pdf)  
     `SHA-256: 3c3b55e217fa2925a970c69505acd943ff945b0f4a64dac002a4ec691b5648fb`
   - Canonical Table TSV: [`artifacts/sampling_frame/dos_reis_2021_table2.tsv`](artifacts/sampling_frame/dos_reis_2021_table2.tsv)  
     `SHA-256: c81654c225c51d43bc4de3a9d373c0b217c66b2d3752e39de5606e35c7fe7736`
4. **High-Documentation Pool Artifacts:**
   - Spec: [`artifacts/sampling_frame/scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json)  
     `SHA-256: ea4d221889e2b7fff2a2b10ce0c035fe748145a8db43e612564f92a27769d5b3`
   - Raw Crossref Response: [`artifacts/sampling_frame/scientific_data_crossref_raw.json`](artifacts/sampling_frame/scientific_data_crossref_raw.json)  
     `SHA-256: 854f7da7770d68a564b31a2b242d22d103b31b205c928bb13c84225c3ee8c83f`
   - Candidates TSV: [`artifacts/sampling_frame/scientific_data_candidates.tsv`](artifacts/sampling_frame/scientific_data_candidates.tsv)  
     `SHA-256: 6002ee04b5c984a8700e09546c9e5fcdc4d9c87076a5baf00a8c0029fc44f5db`
5. **Epistemic Disclosures:** [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md)
6. **Execution Invariants & State:** [`PREREGISTRATION.md`](PREREGISTRATION.md) & [`STATUS.md`](STATUS.md)

---

## 4. Execution Invariants Maintained
- Zero target deposit repository URLs opened pre-freeze (`target_deposit_inspections_pre_freeze: 0`).
- Execution state HALT.
