---
project: battery-deposit-semantics-s1
phase: terminal_instrument_invalid
owner: Ivan
analyst: Sol
ops: Ananke
gate: formal Gate (external)
instrument_file: INSTRUMENT.md
sampling_frame_file: SAMPLING_FRAME.md
pre_freeze_exposure_file: PRE_FREEZE_EXPOSURE.md
prereg_frozen: true
candidate_freeze_commit: "b8aa8a71f2bfa76ebb298e18b6803428462757c6"
governing_freeze_commit: "4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126"
verdict: INSTRUMENT_INVALID
calibration_sample_size: 2
confirmatory_sample_size: 3
calibration_case: "Sandia (observed case / preliminary calibration)"
calibration_positive: "Chung 2021 (DOI: 10.1038/s41597-021-00954-3)"
confirmatory_high_doc_control_status: NOT_ADJUDICATED
confirmatory_targets_status: NOT_ADJUDICATED
target_deposit_inspections_pre_freeze: 0
---

## Instance Summary
This repository contains the preregistration specification and measurement instrument for auditing export semantics and reproducibility boundaries across public lithium-ion battery degradation datasets.

### Terminal State
- **Phase:** Execution Terminated / Instrument Invalid (`INSTRUMENT_INVALID`).
- **Terminal Cause:** Pre-registered validity criterion failed on `CALIBRATION_POSITIVE` (Chung 2021). Parameter P5 was formulated as a compound requirement (cadence AND operation coverage verification); while cadence ($\Delta t = 10\text{ s}$) was documented, operation coverage verification was not explicitly documented in pinned space. Chung resolved 2/3 pre-asserted parameters (P1, P3), falling short of the required 3/3 (`RESOLVED_IN_PINNED_SPACE`).
- **Confirmatory Execution:** Permanently halted. Confirmatory observation units (`CONFIRMATORY_HIGH_DOC_CONTROL`, `CONFIRMATORY_TARGET_1`, `CONFIRMATORY_TARGET_2`) were accessioned at Level-0 pre-calibration but remain unadjudicated semantically.
- **Verdict-Bearing Results:** NONE.
- **Exploratory Trace:** Pinned documentation in Nature Scientific Data explicitly resolved logging cadence but omitted a formal protocol for verifying complete temporal operation coverage.
- **Successor Governance:** All S1 authors, specifiers, and contributing reviewers are role-conflicted under independence rules. Any successor instance (S2) must be independently assessed and specified by an unconflicted constructor.

