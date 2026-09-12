# Preregistration: Battery Deposit Export Semantics Audit (S1)

- **Instance ID:** `battery-deposit-semantics-s1`
- **Owner / Operator:** Ivan
- **Analyst:** Sol
- **Ops Custodian:** Ananke
- **Reviewer / Gate:** External Formal Gate

---

## 1. Objective & Research Question
Can publicly distributed commercial lithium-ion battery degradation datasets unambiguously resolve the export semantics required for reproducible throughput / Equivalent Full Cycle (EFC) reconstruction using strictly their public pinned documentation, or does complete semantic resolution require private correspondence with data depositors?

---

## 2. Core Methodological Hypotheses & Calibration Status (G-1)

1. **Hypothesis 1 (Public Document Boundary):** Public battery degradation datasets published without formal data descriptor mandates do not resolve all applicable reconstruction parameters within their Tier 1–3 search space.
2. **Hypothesis 2 (Correspondence Necessity & Uniform Outreach):** Complete reproducible reconstruction of unstandardized battery exports requires off-artifact depositor correspondence to resolve missing conventions. To test this uniformly, every evaluated confirmatory dataset receives an identical standardized 6-question inquiry with a 14-calendar-day response window, measuring two distinct dimensions:
   - *Dimension A:* Public pinned-space semantic completeness.
   - *Dimension B:* External depositor response completeness.
3. **Instrument Calibration & Consistency (G-1 Recognition):**
   - **Internal Consistency Benchmark (`CALIBRATION_POSITIVE` — Chung 2021):** Because the explicit documentation of Chung (2021) for P1, P3, and P5 was pre-asserted during preliminary review, this case serves as a non-blind consistency test. The instrument must faithfully register `RESOLVED_IN_PINNED_SPACE` for these parameters; failure to do so results in **`INSTRUMENT_INVALID`**.
   - **Absence of Blind Instrument Falsification:** This instance makes **no claim** that the instrument has been demonstrated to be blind-falsifiable.
   - **Empirical Confirmatory Control (`CONFIRMATORY_HIGH_DOC_CONTROL`):** The candidate selected deterministically from the frozen *Nature Scientific Data* pool is an empirical confirmatory evaluation. Any outcome (`RESOLVED`, `UNDERDETERMINED`, or `NOT_FOUND_IN_PINNED_SPACE`) is admissible as a domain finding regarding the efficacy of data descriptor mandates, and does **NOT** invalidate the instrument.

---

## 3. Preregistered Invariants & Prohibitions
1. **Zero Pre-Freeze URL Inspection:** No URL, repository landing page, data file, or supplementary link belonging to any Table 2 candidate or High-Doc candidate shall be accessed or evaluated prior to freeze ratification.
2. **Zero Post-Hoc Model Fitting:**
   - Parameter definitions in `INSTRUMENT.md` and reconstruction pathways (A, B, C) are frozen.
   - Applicability gates must be decided exclusively from physical schema inspection prior to documentary search.
   - Deterministic hash selection from the frozen candidate pools must be executed strictly without manual intervention or discretion.
3. **Zero Paraphrasing / Synthetic Evidence:**
   - All evidentiary citations must be literal excerpts with exact section, table, or line locators.
4. **Append-Only Failure Tracking:**
   - Any deviations, attrition events, or drift findings must be logged in `FAILURES.md` without history rewrites.
