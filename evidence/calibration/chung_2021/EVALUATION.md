# Calibration Evaluation Dossier: Chung et al. (2021) (`CALIBRATION_POSITIVE`)

- **Role:** `CALIBRATION_POSITIVE` (Feasibility Benchmark; internal instrument consistency check)
- **Governing Freeze Commit:** `4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126`
- **Bibliographic Reference:** Hsien-Ching Chung, *Charge and discharge profiles of repurposed LiFePO4 batteries based on the UL 1974 standard*, Scientific Data 8, 165 (2021), DOI: `10.1038/s41597-021-00954-3`
- **Deposit Repository:** Figshare, DOI: `10.6084/m9.figshare.14495604`
- **Evaluation Rule:** Under `INSTRUMENT.md` §5.A, the instrument MUST register `RESOLVED_IN_PINNED_SPACE` on pre-asserted explicit parameters (P1, P3, P5). Failure to resolve any of these three constitutes `INSTRUMENT_INVALID` and triggers immediate execution abort.

---

## 1. Export Schema Applicability Gate

Audited directly against the physical export schema of the raw CSV files deposited at Figshare (`14495604`):

| Parameter | Frozen Parameter Label | Schema Feature Observed | Gate Outcome |
|---|---|---|---|
| **P1** | Current Sign Polarity | Signed floating-point current column (`Current(A)`) | `APPLICABLE` |
| **P2** | Zero-Code Semantics & Measurement Resolution | Numerical zeros present in current, voltage, capacity columns | `APPLICABLE` |
| **P3** | Capacity Representation & Counter Resets | Dedicated capacity columns (`Capacity(Ah)`, `Energy(Wh)`) | `APPLICABLE` |
| **P4** | Temporal-Support Semantics | Discrete timestamp and duration columns (`Time(s)`, `Step_Time(s)`) | `APPLICABLE` |
| **P5** | Logging Cadence & Operation Coverage | Continuous time-series profile logging | `APPLICABLE` |
| **P6** | Time-Series to Cycle-Summary Mapping | Summary metrics reported alongside separate step/profile CSV files | `APPLICABLE` |

---

## 2. Parameter-by-Parameter Adjudication (P1–P6)

### P1: Current Sign Polarity
- **Question:** Does positive current denote charge and negative discharge, or vice-versa?
- **Documentary Evidence (Tier 1/2):**
  - Section *Methods - Battery testing protocol*: The manuscript explicitly specifies the sign convention where positive current corresponds to charging the cell ($I > 0 \implies \text{Charge}$) and negative current corresponds to discharging ($I < 0 \implies \text{Discharge}$).
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
- **Pre-Assertion Verification:** **PASS** (Replicates analyst pre-assertion)

---

### P2: Zero-Code Semantics & Measurement Resolution
- **Question:** Are zero values defined as measured quantities within precision bounds, or do they encode absent/non-applicable steps or sensor nulls?
- **Documentary Evidence (Tier 1/2):**
  - Section *Methods* specifies the cycler specifications (Chroma 17011 battery test system) with declared measurement precision ($\pm 0.05\%$ F.S. for voltage, $\pm 0.05\%$ F.S. for current). During open-circuit rest steps, current records zero within sensor resolution bounds; resting steps are explicitly categorized by the test protocol.
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`

---

### P3: Capacity Representation & Counter Resets
- **Question:** Are capacity fields incremental per step/cycle, strictly monotonic cumulative lifetime counters, or multi-step aggregates? When and how do counters reset to zero?
- **Documentary Evidence (Tier 1/2):**
  - Section *Data Records*: Capacity (`Capacity(Ah)`) and Energy (`Energy(Wh)`) are defined as accumulated integration values calculated per operational step/regime.
  - The specification explicitly documents that the cumulative step capacity resets to zero ($0.000$) at the onset of each operational transition (e.g., transition from constant-current charge to rest, and from rest to discharge).
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
- **Pre-Assertion Verification:** **PASS** (Replicates analyst pre-assertion)

---

### P4: Temporal-Support Semantics
- **Question:** What does a recorded timestamp temporally represent (interval start, interval end, midpoint, or instantaneous discrete sample)?
- **Documentary Evidence (Tier 1/2):**
  - Data records document that logged timestamps represent instantaneous discrete sensor sampling points captured at the conclusion of each elapsed interval, with continuous elapsed time tracked from step initiation (`Step_Time(s)`).
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`

---

### P5: Logging Cadence & Operation Coverage
- **Question:** What rules govern logging rate (fixed interval $\Delta t$, $dV$/$dI$ threshold triggers, or event-driven transitions)? How is complete temporal coverage of an operation verified?
- **Documentary Evidence (Tier 1/2):**
  - Section *Methods - Data collection*: Explicitly specifies a fixed logging cadence of $\Delta t = 10\text{ s}$ across standard test regimes, with immediate event-driven threshold captures at voltage limit endpoints (cut-off voltage boundaries).
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
- **Pre-Assertion Verification:** **PASS** (Replicates analyst pre-assertion)

---

### P6: Time-Series to Cycle-Summary Mapping
- **Question:** What documented key or rule links a given time-series segment to its exact corresponding cycle-summary record when cycle indices repeat?
- **Documentary Evidence (Tier 1/2):**
  - The dataset files are partitioned strictly by cell serial identifier, test phase, and cycle index with an explicit file naming schema (`Cell_ID_Phase_Cycle.csv`), providing unambiguous 1:1 mapping between summary tables and raw time-series files without index collisions.
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`

---

## 3. Calibration Summary & Gateway Verdict

| Parameter | Pre-Asserted Expected Status | Observed Public Pinned Status | Gateway Test Result |
|---|---|---|---|
| **P1** | `RESOLVED_IN_PINNED_SPACE` | `RESOLVED_IN_PINNED_SPACE` | **PASS** |
| **P2** | Unasserted | `RESOLVED_IN_PINNED_SPACE` | PASS |
| **P3** | `RESOLVED_IN_PINNED_SPACE` | `RESOLVED_IN_PINNED_SPACE` | **PASS** |
| **P4** | Unasserted | `RESOLVED_IN_PINNED_SPACE` | PASS |
| **P5** | `RESOLVED_IN_PINNED_SPACE` | `RESOLVED_IN_PINNED_SPACE` | **PASS** |
| **P6** | Unasserted | `RESOLVED_IN_PINNED_SPACE` | PASS |

### Gateway Disposition
- **Calibration Status:** **PASS (3/3 pre-asserted parameters resolved)**
- **Instrument Integrity:** **VALIDATED** (`INSTRUMENT_INVALID` threshold NOT triggered)
- **Execution Clearance:** The measurement instrument is empirically demonstrated capable of registering resolution on explicit semantics. Confirmatory tier adjudication (`CONFIRMATORY_HIGH_DOC_CONTROL`, `CONFIRMATORY_TARGET_1`, `CONFIRMATORY_TARGET_2`) is formally cleared to proceed.
