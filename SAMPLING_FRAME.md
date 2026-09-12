# Sampling Frame & Dataset Selection Protocol (S1)

This specification establishes the external sampling frame, eligibility criteria, deterministic hash-ranking algorithm, and control pool for instance `battery-deposit-semantics-s1`.

---

## 1. External Denominator & Canonical Sampling Source (B-1, G-3)

To eliminate selection bias, the target sampling frame is drawn strictly from an external, peer-reviewed survey published prior to the design of this instrument:
- **Bibliographic Work:** Gonçalo dos Reis, Calum Strange, Mohit Yadav, Shawn Li, *Lithium-ion battery data and where to find it*, Energy and AI 5 (2021), 100081, DOI: `10.1016/j.egyai.2021.100081`.
- **Canonical S1 Sampling Artifact (G-3):** The pinned accepted-manuscript PDF, [`artifacts/sampling_frame/dos_reis_2021_accepted_manuscript.pdf`](artifacts/sampling_frame/dos_reis_2021_accepted_manuscript.pdf) (SHA-256: `3c3b55e217fa2925a970c69505acd943ff945b0f4a64dac002a4ec691b5648fb`), Table 2 ("Overview of cycle ageing datasets"), page 12.
- **Canonical Table Artifact:** [`artifacts/sampling_frame/dos_reis_2021_table2.tsv`](artifacts/sampling_frame/dos_reis_2021_table2.tsv) (SHA-256: `c81654c225c51d43bc4de3a9d373c0b217c66b2d3752e39de5606e35c7fe7736`).
- **Transcription Protocol:**
  - **Forward-fill rule:** For continuation rows belonging to the same institution header (NASA, CALCE, TRI), `Location with weblink` is forward-filled from the preceding header row.
  - **Cell descriptor rule:** Empty cells (e.g., TRI row 2) remain strictly empty strings (`""`) unless the table text explicitly provides a distinct cell descriptor.
- **Sampling Unit:** A unique dataset row in Table 2 (17 total rows in population; not an institution or research group).

---

## 2. Eligibility Criteria & Filtering Rule

A Table 2 row is deemed eligible for inclusion in the confirmatory target candidate set if and only if all of the following conditions are met:
1. **Ageing Classification:** The entry represents commercial cell cycle-ageing data.
2. **Signal Completeness:** The "Data given" column explicitly includes both voltage ($V$) and current ($I$).
3. **Public Availability Indicator:** A public dataset URL or institutional location is provided.
4. **Mandatory Exclusion:** Any row corresponding to the Sandia commercial cell dataset is strictly excluded, as it serves as the inductive `CALIBRATION_CASE`.

---

## 3. Deterministic Selection Algorithm (Hash-Sort)

To ensure zero discretion in dataset selection, candidate rows are ranked using a deterministic hash function:

### A. Canonical Key Construction
For each eligible Table 2 row:
$$\text{canonical\_key} = \text{lower}(\text{strip}(\text{Location})) \,\|\, \text{"|"} \,\|\, \text{lower}(\text{strip}(\text{Paper Ref})) \,\|\, \text{"|"} \,\|\, \text{lower}(\text{strip}(\text{Cell descriptor}))$$

### B. Selection Score
$$\text{selection\_score} = \text{SHA256}(\text{"battery-deposit-semantics-s1|10.1016/j.egyai.2021.100081|"} \,\|\, \text{canonical\_key})$$

### C. Ranking & Selection
1. All eligible rows from the canonical population are sorted in ascending lexicographical order by `selection_score`.
2. The first two eligible entries become:
   - `CONFIRMATORY_TARGET_1`
   - `CONFIRMATORY_TARGET_2`

### D. Attrition Handling (`FRAME_ATTRITION`)
If a selected repository URL is permanently unreachable at Level-0 verification (404, repository retired, domain defunct):
- It is formally logged as `FRAME_ATTRITION` in `FAILURES.md`.
- The next eligible row in ascending `selection_score` order is selected as the replacement.
- Documentation quality, format complexity, or perceived difficulty of adjudication shall never serve as grounds for dataset replacement.

---

## 4. Control Architecture & Pool Specification (G-2)

The evaluation set cleanly separates calibration benchmarks from the confirmatory analysis sample:

### A. Calibration Benchmarks (Excluded from Confirmatory Sample Size)
1. **Sandia Commercial Degradation (`CALIBRATION_CASE`):**
   - Inductive case study where preliminary boundary questions were formulated.
2. **Chung et al. (2021) (`CALIBRATION_POSITIVE`):**
   - *Scientific Data* 8, 165 (2021), DOI: `10.1038/s41597-021-00954-3`.
   - Used exclusively to verify instrument consistency on known-explicit semantics (P1, P3, P5).

### B. Confirmatory High-Documentation Control (`CONFIRMATORY_HIGH_DOC_CONTROL`) (G-2, G-4)
- **Specification:** Pinned by [`artifacts/sampling_frame/scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json).
- **Frozen Crossref Response:** [`artifacts/sampling_frame/scientific_data_crossref_raw.json`](artifacts/sampling_frame/scientific_data_crossref_raw.json) (36 total items).
- **Frozen Eligibility Adjudication:** [`artifacts/sampling_frame/scientific_data_eligibility.tsv`](artifacts/sampling_frame/scientific_data_eligibility.tsv) (SHA-256: `0f0bbbbff910fbcb22d19f691751861ad3b282eed1c77193a6e440389618bd59`).
  - All 36 items explicitly classified: **4 `IN_SCOPE`**, **3 `INSUFFICIENT_METADATA_TO_CLASSIFY`**, **29 `OUT_OF_SCOPE`**.
  - **Index-Layer Finding:** 3 of 36 records (8.3%) omit critical domain signals (chemistry or test regime) from title metadata, requiring abstain disposition under strict pre-freeze rules.
- **Frozen Candidates TSV:** [`artifacts/sampling_frame/scientific_data_candidates.tsv`](artifacts/sampling_frame/scientific_data_candidates.tsv) (SHA-256: `f4299bfed812cd55446fe182b6d233b4a89a21fa9a23a465a2a29b56032bb89f`) (4 in-scope items ranked deterministically by selection score).
- **Comprehensive Artifact Checksums:** Verified against [`artifacts/sampling_frame/SHA256SUMS`](artifacts/sampling_frame/SHA256SUMS).
- **Mandatory Exclusion:** Chung et al. (2021) is strictly barred from the candidate pool.
- **Deterministic Selection:** The top-ranked in-scope entry in `scientific_data_candidates.tsv` (`10.1038/s41597-024-03831-x` — *Comprehensive battery aging dataset: capacity and impedance fade measurements of a lithium-ion NMC/C-SiO cell*) becomes `CONFIRMATORY_HIGH_DOC_CONTROL` upon freeze ratification.
- **Limitation Notice:** Requiring the title to prove both chemistry and regime selects datasets with explicit titles, potentially correlating with documentation care; it is not an unconstrained random draw from all descriptors. Target datasets from Table 2 do not share this constraint.
- **Blindness Invariant:** Target repository contents, time-series data files, and README assets of the selected candidate remain strictly unopened prior to execution.

---

## 5. Sample Size Partition ($n_{\text{confirmatory}} = 3$) (B-6)

To prevent known-good calibration cases from artificially inflating confirmatory documentation rates, sample accounting is strictly partitioned:
- **Calibration Set ($n = 2$):**
  - $1 \times \text{CALIBRATION\_CASE}$ (Sandia)
  - $1 \times \text{CALIBRATION\_POSITIVE}$ (Chung 2021)
- **Confirmatory Analysis Set ($n_{\text{confirmatory}} = 3$):**
  - $1 \times \text{CONFIRMATORY\_HIGH\_DOC\_CONTROL}$ (Nature Scientific Data candidate rank 1)
  - $1 \times \text{CONFIRMATORY\_TARGET\_1}$ (dos Reis Table 2 rank 1)
  - $1 \times \text{CONFIRMATORY\_TARGET\_2}$ (dos Reis Table 2 rank 2)

**Total Evaluated Units:** 5 datasets across both tiers; statistical and synthesis claims are reported strictly over the $n_{\text{confirmatory}} = 3$ set.
