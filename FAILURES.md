# Failures & Deviations Log

## F-001: Model Erroneous Citation Intercepted Pre-Freeze
- **Date:** 2026-09-12
- **Severity:** Pre-Freeze Citation Defect (Intercepted)
- **Description:** An incorrect DOI (`10.1016/j.est.2021.102250`, purporting to be *Journal of Energy Storage* / *dos Reis et al.*) was emitted during agent planning.
- **Resolution:** Intercepted and rejected during pre-freeze review by Sol and Reviewer. The correct publication was verified against the publisher record: *Energy and AI*, Vol. 5, Article 100081 (2021), DOI: `10.1016/j.egyai.2021.100081`. Zero repository artifacts rely on the erroneous citation.

## F-002: Synthetic Secondary Sampling Frame Materialization Attempt (Intercepted)
- **Date:** 2026-09-12
- **Severity:** Methodological / Provenance Defect (Intercepted Pre-Freeze)
- **Description:** The agent generated a draft `dos_reis_2021_table2.tsv` using memory-based secondary summaries after failing to retrieve the online document directly, producing factual discrepancies in cell counts and references (e.g., NASA cell counts, reference indices).
- **Resolution:** Intercepted by Sol and Operator prior to freeze. The draft was discarded. The authentic peer-reviewed accepted manuscript PDF (`Batteries_Li_ion_battery_data_and_where_to_find_it_final_draft_.pdf`, SHA-256 `3c3b55e2...`) was placed into `artifacts/sampling_frame/`, and an exact, literal, word-for-word TSV transcription was extracted directly from Table 2 on page 12 under strict forward-fill rules.
