# Calibration Evaluation Dossier (v2): Chung et al. (2021) (`CALIBRATION_POSITIVE`)

- **Role:** `CALIBRATION_POSITIVE` (Feasibility Benchmark; internal instrument consistency check)
- **Governing Freeze Commit:** `4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126`
- **Bibliographic Reference:** Hsien-Ching Chung, *Charge and discharge profiles of repurposed LiFePO4 batteries based on the UL 1974 standard*, Scientific Data 8, 165 (2021), DOI: `10.1038/s41597-021-00954-3`
- **Pinned Primary Deposit:** Figshare, DOI: `10.6084/m9.figshare.14495604` (Metadata stub / redirect record)
- **Underlying Primary Repository:** Open Science Framework (OSF), DOI: `10.17605/OSF.IO/PFH3G` (Node `pfh3g`)
- **Remediation Notice:** This dossier (v2) supersedes `EVALUATION.md` (v1, commit `c2d7ecf87a7d6b247bf8013f37a41be92ac97834`) pursuant to failure record `F-006` in `FAILURES.md`. All historical artifacts are preserved append-only.

---

## 1. Export Schema & Custody Audit

Audited directly against authentic primary artifacts sealed in `evidence/calibration/chung_2021/raw_schema/`:
- Figshare Article API: `figshare_14495604_api.json`
- OSF Storage Root Manifest: `osf_pfh3g_root_manifest.json`
- Authentic Raw Profile Sample: `P1_20191021090628_sample.csv` (`P1_20191021090628.csv`, 186,520 bytes, 3,101 rows)

### Authentic Raw CSV Header
```text
Data point,Step,Step time,Voltage(V),Current(A),Power(W),Temperature(°C),Capacity(mAh),Energy(Wh),Total time,End status
```

### Schema Applicability Matrix
| Parameter | Frozen Parameter Label | Schema Column / Feature Observed | Applicability Status |
|---|---|---|---|
| **P1** | Current Sign Polarity | `Current(A)` (signed floating-point values) | `APPLICABLE` |
| **P2** | Zero-Code Semantics & Resolution | Numerical zeros across float columns; cycler specs in text | `APPLICABLE` |
| **P3** | Capacity Representation & Resets | `Capacity(mAh)`, `Energy(Wh)`, `Step` index | `APPLICABLE` |
| **P4** | Temporal-Support Semantics | `Step time`, `Total time` (`hh:mm:ss`) | `APPLICABLE` |
| **P5** | Logging Cadence & Coverage | Monotonic `Data point` integer series; `t_rec` in text | `APPLICABLE` |
| **P6** | Time-Series to Summary Mapping | 17-digit file code (`P1_20191021090628.csv`); cell folders | `APPLICABLE` |

---

## 2. Parameter-by-Parameter Adjudication (P1–P6)

### P1: Current Sign Polarity
- **Target Question:** Does positive current denote charge and negative discharge, or vice-versa?
- **Documentary Evidence (Tier 1/2 Text):**
  - Section *Methods - UL 1974*, line 1076:
    > *"where $\text{SOC}(t_0)$ is the previous SOC of the battery, $\text{Cap}$ is the ampere hour capacity of the fully charged battery, and $I(\tau)$ is the current with positive (negative) value for discharge (charge)..."*
  - Section *Methods - Standard charge and discharge processes of Li-ion battery*:
    > *"(4) The signs for discharge and charge constant currents ($I_{c1}, I_{c2}$) might choose as $(-, +)$, $(+, -)$, or $(+, +)$."*
- **Physical Verification (Raw CSV Sample):**
  - In `P1_20191021090628_sample.csv`, Step 7 corresponds to CC discharge. Current values are recorded as positive ($+7.493\text{ A}$), while voltage decreases monotonically from $3.2679\text{ V}$ to $3.2431\text{ V}$.
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
  - **Established Rule:** **Positive Current = Discharge ($I > 0$); Negative Current = Charge ($I < 0$).**
- **Pre-Assertion Verification:** **PASS** (Replicates analyst pre-assertion that polarity is explicitly resolved in pinned documentation).

---

### P2: Zero-Code Semantics & Measurement Resolution
- **Target Question:** Are zero values defined as measured quantities within precision bounds, or do they encode absent/non-applicable steps or sensor nulls?
- **Documentary Evidence (Tier 1/2 Text):**
  - Section *Methods - Measurement equipment and data collection*:
    > *"The charge and discharge performance of the batteries were evaluated using the battery test system (CTE-MCP-5082020A, Chen Tech Electric Mfg. Co., Ltd., Taiwan)... Output data was saved in the format of csv file..."*
  - The manuscript does not define numerical zero codes or declare explicit numeric sensor epsilon null bands. The claim of "Chroma 17011" in v1 was factually erroneous (F-006).
- **Adjudication Outcome:** `NOT_FOUND_IN_PINNED_SPACE` / `UNVERIFIED`
- **Gateway Impact:** Unasserted parameter; does not block calibration gateway.

---

### P3: Capacity Representation & Counter Resets
- **Target Question:** Are capacity fields incremental per step/cycle, strictly monotonic cumulative lifetime counters, or multi-step aggregates? When and how do counters reset to zero?
- **Documentary Evidence (Tier 1/2 Text):**
  - Section *Data Records*:
    > *"The data at the time stamp has two types: (1) current and (2) accumulated data. The former indicates that the data is measured at the time stamp, such as voltage, current, power, and temperature. The latter indicates that the data is the sum of the current and previous data, such as capacity and energy. Hence, the value of capacity (energy) stands for the amount of mAh (Wh) stored at the time stamp, and it will return to zero at the beginning of each step."*
- **Physical Verification (Raw CSV Sample):**
  - At the onset of Step 1 (`Data point` 1): `Capacity(mAh) = 0`, `Energy(Wh) = 0`.
  - At the onset of Step 2 (`Data point` 7): `Capacity(mAh) = 0`, `Energy(Wh) = 0`.
  - At the onset of Step 3: `Capacity(mAh)` resets to `0`.
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
  - **Established Rule:** **Capacity and Energy are accumulated quantities that strictly reset to zero at the beginning of each operational step.**
- **Pre-Assertion Verification:** **PASS** (Replicates analyst pre-assertion).

---

### P4: Temporal-Support Semantics
- **Target Question:** What does a recorded timestamp temporally represent (interval start, interval end, midpoint, or instantaneous discrete sample)?
- **Documentary Evidence (Tier 1/2 Text):**
  - Section *Data Records*:
    > *"The data at the time stamp has two types: (1) current and (2) accumulated data. The former indicates that the data is measured at the time stamp..."*
  - While timestamps (`Step time`, `Total time`) are described as samples measured at the time stamp, the text does not formally define the topological interval closure (e.g., left-closed vs. right-closed integration interval).
- **Adjudication Outcome:** `UNDERDETERMINED_IN_PINNED_SPACE`
- **Gateway Impact:** Unasserted parameter; does not block calibration gateway.

---

### P5: Logging Cadence & Operation Coverage
- **Target Question:** What rules govern logging rate (fixed interval $\Delta t$, $dV$/$dI$ threshold triggers, or event-driven transitions)? How is complete temporal coverage of an operation verified?
- **Documentary Evidence (Tier 1/2 Text):**
  - Section *Methods - Measurement equipment and data collection*:
    > *"The data was logged every ten seconds ($t_{\text{rec}} = 10\text{ sec}$) by the CTE-Will software (version 1.13tc)."*
  - Section *Methods - Two-tier DC load method*:
    > *"where $t_{\text{rec}}$ is the data recording time interval."*
- **Dual-Conjunct Analysis:**
  - **Conjunct A (Rate Rule):** **RESOLVED.** The text explicitly defines a fixed periodic logging cadence of $\Delta t = 10\text{ s}$ ($t_{\text{rec}} = 10\text{ s}$).
  - **Conjunct B (Operation Coverage Verification):**
    - The raw CSV provides a strictly monotonic integer counter (`Data point` from 1 to 3,100) and step-relative timestamps (`Step time`, `Total time`). Step completions are marked with explicit condition labels in the `End status` column (e.g., `Time`, `Voltage`).
    - *Evidentiary Limitation:* The published manuscript does not describe an independent communication-loss protocol or lost-packet diagnostic for verifying that no packets were dropped. Completeness is verifiable at the physical schema level via the continuity of the integer index and timestamp progression, but lacks a separate textual verification protocol.
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
  - **Established Rule:** **Logging cadence is governed by a strict periodic interval of $\Delta t = 10\text{ s}$. Operation coverage is tracked via continuous step timestamps and monotonic data-point sequences terminating on explicit end-status events.**
- **Pre-Assertion Verification:** **PASS** (Replicates analyst pre-assertion).

---

### P6: Time-Series to Cycle-Summary Mapping
- **Target Question:** What documented key or rule links a given time-series segment to its exact corresponding cycle-summary record when cycle indices repeat?
- **Documentary Evidence (Tier 1/2 Text):**
  - Section *Data Records*:
    > *"An 18-digit code is used to mark the repurposed battery cell and the file folder of the dataset in the data repository, including the 2-digit vendor code, 1-digit battery type code, 2-digit specification code, 6-digit disassembling date code, and 7-digit serial number code... The csv file name is labeled by a 17-digit code, including the 2-digit procedure code, 14-digit date and time code (indicating the time of the start of the test), as well as 1-digit underline separating the two codes..."*
- **Adjudication Outcome:** `RESOLVED_IN_PINNED_SPACE`
  - **Established Rule:** **Time-series profiles are deterministically bound to cells and test runs via hierarchical folder structure (18-digit cell code) and file naming (17-digit procedure and start-timestamp code).**

---

## 3. Calibration Summary & Gateway Verdict

| Parameter | Pre-Asserted Expected Status | Observed Public Pinned Status (v2) | Gateway Test Result |
|---|---|---|---|
| **P1** (Current Polarity) | `RESOLVED_IN_PINNED_SPACE` | `RESOLVED_IN_PINNED_SPACE` (Pos=Discharge, Neg=Charge) | **PASS** |
| **P2** (Zero-Code / Resolution) | Unasserted | `NOT_FOUND_IN_PINNED_SPACE` (Withdrawn) | PASS (Non-blocking) |
| **P3** (Capacity Resets) | `RESOLVED_IN_PINNED_SPACE` | `RESOLVED_IN_PINNED_SPACE` (Reset to zero per step) | **PASS** |
| **P4** (Temporal Support) | Unasserted | `UNDERDETERMINED_IN_PINNED_SPACE` | PASS (Non-blocking) |
| **P5** (Cadence / Coverage) | `RESOLVED_IN_PINNED_SPACE` | `RESOLVED_IN_PINNED_SPACE` ($\Delta t = 10\text{ s}$; continuous index) | **PASS** |
| **P6** (Mapping / Key) | Unasserted | `RESOLVED_IN_PINNED_SPACE` (17-digit procedure timestamp) | PASS (Non-blocking) |

### Gateway Disposition
- **Calibration Status:** **PASS (3/3 pre-asserted parameters resolved)**
- **Instrument Feasibility:** **CONFIRMED** (`INSTRUMENT_INVALID` threshold NOT triggered).
- **Evidentiary Integrity:** Authentic OSF raw CSV schema custody sealed under freeze commit `4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126`.
- **Execution Clearance:** Confirmatory tier semantic adjudication (`CONFIRMATORY_HIGH_DOC_CONTROL`, `CONFIRMATORY_TARGET_1`, `CONFIRMATORY_TARGET_2`) is formally unlocked.
