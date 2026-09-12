# Failures & Deviations Log

## F-001: Model Erroneous Citation Intercepted Pre-Freeze
- **Date:** 2026-09-12
- **Severity:** Pre-Freeze Citation Defect (Intercepted)
- **Description:** An incorrect DOI (`10.1016/j.est.2021.102250`, purporting to be *Journal of Energy Storage* / *dos Reis et al.*) was emitted during agent planning.
- **Resolution:** Intercepted and rejected during pre-freeze review by Sol and Reviewer. The correct publication was verified against the publisher record: *Energy and AI*, Vol. 5, Article 100081 (2021), DOI: `10.1016/j.egyai.2021.100081`. Zero repository artifacts rely on the erroneous citation.

## F-002: Synthetic Secondary Sampling Frame Materialization Attempt (Intercepted)
- **Date:** 2026-09-12
- **Severity:** Methodological / Provenance Defect (Intercepted Pre-Freeze)
- **Description:** The agent generated a draft `dos_reis_2021_table2.tsv` using memory-based secondary summaries after failing to retrieve the online document directly, producing factual discrepancies in cell counts and references.
- **Resolution:** Intercepted by Sol and Operator prior to freeze. The draft was discarded. The authentic peer-reviewed accepted manuscript PDF (`Batteries_Li_ion_battery_data_and_where_to_find_it_final_draft_.pdf`, SHA-256 `3c3b55e2...`) was placed into `artifacts/sampling_frame/`, and an exact, literal, word-for-word TSV transcription was extracted directly from Table 2 on page 12 under strict forward-fill rules.

## F-003: High-Doc Control Domain Leakage & Stale Checksum (Intercepted on Terminal Gate G-4 / G-5)
- **Date:** 2026-09-12
- **Severity:** Domain Integrity & Checksum Verification Defect (Intercepted Pre-Freeze)
- **Description:** 
  1. A naive keyword filter (`battery` and `cycling`/`degradation`) allowed non-lithium chemistry (zinc-oxygen, zinc-air) and non-cycling papers (battery recycling due to `recycling ⊃ cycling`) into the High-Doc candidate pool, placing Dongmo et al. (zinc-oxygen) at Rank 1.
  2. The SHA-256 checksum for `scientific_data_pool_spec.json` declared in `CANDIDATE.md` was stale.
- **Resolution:** Intercepted by Gate review. Rather than replacing with another fragile regex, the entire 36-item Crossref population was explicitly adjudicated item-by-item in `artifacts/sampling_frame/scientific_data_eligibility.tsv` against a strict lithium-ion cycling domain criterion, isolating exactly 7 `IN_SCOPE` datasets. The candidate pool was re-ranked deterministically over in-scope items, placing lithium-ion characterization dataset `10.1038/s41597-025-05725-y` at Rank 1. All checksums were recomputed and unified in `artifacts/sampling_frame/SHA256SUMS`.

## F-004: Target Duplicate Observation Unit & High-Doc Cell/Pack Scope Misalignment (Intercepted Pre-Freeze)
- **Date:** 2026-09-12
- **Severity:** Sampling Design & Observation-Unit Defect (Intercepted Pre-Freeze)
- **Description:**
  1. **Target Observation-Unit Collapse (N-1):** Deterministic ranking of dos Reis Table 2 eligible rows placed TRI row 2 (Ref [72]) at Rank 1 and TRI row 1 (Ref [6]) at Rank 2. Both point to the exact same canonical repository location (`TRI [71, URL]`), collapsing confirmatory observation units to $n=1$.
  2. **High-Doc Domain Scope Dropping Cells/Packs (N-2):** Title-evidentiary filter permitted materials/component cycling studies without requiring full cells or packs, admitting `10.1038/s41597-022-01217-5` (Al2O3-coated cathode material cycling).
- **Resolution:**
  1. Formalized observation unit as unique canonical deposit location (`lower(strip(Location with weblink))`). Instituted sampling without replacement at observation-unit level: Rank 1 selected (`TRI [71, URL]` / `[72]`), Rank 2 skipped as `SAME_DEPOSIT_LOCATION_DUPLICATE`, and next eligible entry with distinct observation unit (`KIT [86, URL]` / `[8]`) selected as `CONFIRMATORY_TARGET_2`.
  2. Aligned High-Doc scope criterion to strictly require empirical cycling/aging/degradation of rechargeable lithium-ion cells or packs, reclassifying `10.1038/s41597-022-01217-5` to `OUT_OF_SCOPE` (in-scope count updated from 4 to 3; Rank 1 invariant: `10.1038/s41597-024-03831-x`).
  3. Recomputed and synchronized all affected artifacts and authoritative checksums.
