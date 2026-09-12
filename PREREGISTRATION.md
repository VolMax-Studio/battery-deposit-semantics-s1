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

## 2. Core Methodological Hypotheses
1. **Hypothesis 1 (Public Document Boundary):** Public battery degradation datasets published without formal data descriptor mandates do not resolve all applicable reconstruction parameters within their Tier 1–3 search space.
2. **Hypothesis 2 (Correspondence Necessity):** Complete reproducible reconstruction of unstandardized battery exports requires off-artifact depositor correspondence to resolve missing conventions.
3. **Instrument Falsifiability:** Datasets with formal Data Descriptors (`CONFIRMATORY_POSITIVE`) will resolve the minimal necessary reconstruction parameters $\{P1, P3\}$, establishing that the instrument does not artificially suppress positive documentation findings.

---

## 3. Preregistered Invariants & Prohibitions
1. **Zero Pre-Freeze URL Inspection:** No URL, repository landing page, data file, or supplementary link belonging to any Table 2 candidate entry shall be accessed or evaluated prior to freeze ratification.
2. **Zero Post-Hoc Model Fitting:**
   - Parameter definitions in `INSTRUMENT.md` are frozen.
   - Applicability gates must be decided exclusively from physical schema inspection prior to documentary search.
   - Deterministic hash selection in `SAMPLING_FRAME.md` must be executed without manual override.
3. **Zero Paraphrasing / Synthetic Evidence:**
   - All evidentiary citations must be literal excerpts with exact section, table, or line locators.
4. **Append-Only Failure Tracking:**
   - Any deviations, attrition events, or drift findings must be logged in `FAILURES.md` without history rewrites.
