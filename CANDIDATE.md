# Candidate Freeze Submission: battery-deposit-semantics-s1 (Round 1 Remediation)

## 1. Candidate Overview
- **Instance:** `battery-deposit-semantics-s1`
- **Submission Type:** Pre-Execution Preregistration Freeze Package (Addressing B-1 through B-8)
- **Governing Protocol:** P10 Strict Boundary Specification

---

## 2. Remediation Inventory (B-1 through B-8)

| Gate Finding | Remediation Action & Implementation | Primary Artifact |
|---|---|---|
| **B-1** | Pinned canonical sampling-frame object and machine-readable Table 2 population. | [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md), `artifacts/sampling_frame/` |
| **B-2** | Pinned exact metadata-only query specification and deterministic selection for `CONFIRMATORY_HIGH_DOC_CONTROL`. | [`scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json) |
| **B-3** | Decoupled instrument calibration (`CALIBRATION_POSITIVE`) from empirical control (`CONFIRMATORY_HIGH_DOC_CONTROL`); non-resolution on empirical control is a domain finding, not `INSTRUMENT_INVALID`. | [`INSTRUMENT.md`](INSTRUMENT.md) §5 |
| **B-4** | Replaced universal mathematical necessity claim with explicit reconstruction pathways (Pathway A: continuous integration; Pathway B: cycle summary; Pathway C: cross-level reconciliation). | [`INSTRUMENT.md`](INSTRUMENT.md) §1 |
| **B-5** | Generalized P4 to Temporal-Support Semantics (what timestamps represent across arbitrary schemas). | [`INSTRUMENT.md`](INSTRUMENT.md) §2 (P4) |
| **B-6** | Strictly decoupled calibration cases ($n=2$) from the confirmatory analysis set ($n_{\text{confirmatory}} = 3$). | [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md) §5, [`STATUS.md`](STATUS.md) |
| **B-7** | Explicitly renamed same-analyst re-evaluation to Intra-Adjudicator Repeatability Test. | [`INSTRUMENT.md`](INSTRUMENT.md) §6 |
| **B-8** | Symmetrically defined Tier-2 literature to include both canonical Table-2 `Paper Ref` and Tier-1 direct links. | [`INSTRUMENT.md`](INSTRUMENT.md) §3 |

---

## 3. Pinned Artifact Inventory
1. **Measurement Instrument:** [`INSTRUMENT.md`](INSTRUMENT.md)
2. **Sampling Protocol & Denominator:** [`SAMPLING_FRAME.md`](SAMPLING_FRAME.md)
3. **High-Documentation Pool Spec:** [`artifacts/sampling_frame/scientific_data_pool_spec.json`](artifacts/sampling_frame/scientific_data_pool_spec.json)
4. **Epistemic Disclosures:** [`PRE_FREEZE_EXPOSURE.md`](PRE_FREEZE_EXPOSURE.md)
5. **Execution Invariants & State:** [`PREREGISTRATION.md`](PREREGISTRATION.md) & [`STATUS.md`](STATUS.md)

---

## 4. Execution Invariants Maintained
- Zero target deposit repository URLs opened pre-freeze (`target_deposit_inspections_pre_freeze: 0`).
- Execution state HALT.
