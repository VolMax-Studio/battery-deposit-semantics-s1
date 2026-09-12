# Candidate Freeze Submission: battery-deposit-semantics-s1

## 1. Candidate Overview
- **Instance:** `battery-deposit-semantics-s1`
- **Submission Type:** Pre-Execution Preregistration Freeze Package
- **Governing Protocol:** P10 Strict Boundary Specification

---

## 2. Pinned Artifact Inventory
1. **Measurement Instrument:** [`INSTRUMENT.md`](INSTRUMENT.md)
   - Defines the six export-semantics parameters derived from mathematical necessity for throughput / EFC reconstruction ($\int |I| dt$, $\sum Q_{\text{discharge}}$).
   - Establishes the physical schema **Applicability Gate** prior to documentary adjudication.
   - Pinned 3-Tier Search Space hierarchy and strict stopping rule.
   - Standardized 14-day Uniform Depositor Correspondence Protocol.
   - Falsifiable Instrument Validity Rule ($\{P1, P3\}$ must resolve on `CONFIRMATORY_POSITIVE`).
   - Adjudicator Drift Control protocol with masked re-evaluation.
2. **Sampling Protocol & Denominator:** [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md)
   - Authoritative denominator: dos Reis et al. (2021), *Energy and AI* 5, 100081, Table 2.
   - Deterministic SHA-256 hash-sort algorithm for target dataset selection.
   - Fixed sample size $n = 4$ (1 Calibration Positive, 1 Confirmatory Positive, 2 Confirmatory Targets).
   - Attrition rule (`FRAME_ATTRITION`) preventing discretionary replacement.
3. **Epistemic Disclosures:** [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md)
   - Full disclosure of Sandia inductive calibration history.
   - Itemized pre-freeze assertions on Chung et al. (2021) and mandatory bar from confirmatory pool.
   - Model citation interception log (F-PF-01 / F-001).
4. **Execution Invariants:** [`PREREGISTRATION.md`](PREREGISTRATION.md) & [`STATUS.md`](STATUS.md)
   - Zero target URL inspections executed pre-freeze (`target_deposit_inspections_pre_freeze: 0`).
   - Execution state HALT.

---

## 3. Request for Formal Gate Review
This candidate package is submitted for formal Gate review prior to freeze ratification and target dataset selection.
