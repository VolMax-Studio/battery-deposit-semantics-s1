# Export Semantics Measurement Instrument (S1)

This instrument specifies the formal measurement protocol, decision boundaries, evidentiary search spaces, and validity criteria for auditing export semantics across public battery degradation datasets.

---

## 1. Grounding: Reconstruction Pathways & Required Semantics (B-4)
The six parameters evaluated by this instrument are not arbitrary bureaucratic conventions. They correspond to the information requirements of specific mathematical reconstruction pathways for cumulative throughput and Equivalent Full Cycles (EFC).

Rather than asserting a single universal mathematical necessity, the instrument defines three explicit reconstruction pathways:

### Pathway A: Continuous Raw Time-Series Integration
$$\text{Throughput} = \int_{t_{\text{start}}}^{t_{\text{end}}} |I(t)|\, dt$$
- **Primary Information Requirements:**
  - **P5 (Logging Cadence & Time-Base):** Strict temporal base $\Delta t$ between consecutive samples is mandatory for numerical quadrature.
  - **P2 (Zero Semantics):** Precision and sensor null distinction are necessary to prevent integration bias over resting intervals.
  - *Note:* Sign polarity (P1) is not required because the absolute value $|I(t)|$ eliminates directional sign.

### Pathway B: Cycle-Summary Discharge Throughput
$$\text{Throughput} = \sum_{\text{cycles}} Q_{\text{discharge}}$$
- **Primary Information Requirements:**
  - **P1 (Current Sign Polarity):** Mandatory to separate charge from discharge regimes when processing directional current.
  - **P3 (Capacity Representation & Resets):** Mandatory to distinguish incremental per-cycle capacities from cumulative lifetime counters and define counter reset boundaries.
  - **P4 (Temporal-Support Semantics):** Mandatory to ensure adjacent cycle intervals do not overlap or double-count boundary samples.

### Pathway C: Hybrid / Cross-Level Reconciliation
- **Objective:** Mapping time-series segments to cycle-summary aggregates when verifying published summary statistics.
- **Primary Information Requirements:** Requires the union of Pathways A and B, plus **P6 (Time-Series to Cycle-Summary Mapping)**.

---

## 2. The Six Parameters & Applicability Gates

Prior to documentary adjudication, every parameter is evaluated through an **Applicability Gate** based strictly on the observable physical schema (column names, table layout) of the raw export files:
- `APPLICABLE`: The syntactic schema relies on or contains the structural construct (e.g., columns exist, cyclical aggregates present).
- `NOT_APPLICABLE_TO_EXPORT_SCHEMA`: The export architecture does not utilize the construct (e.g., flat, continuous single-column time series without cycle summary or interval bounds).

If `APPLICABLE`, the documentary search space is audited to produce exactly one of three epistemological outcomes:
1. `RESOLVED_IN_PINNED_SPACE`: Explicit, unambiguous documentary specification exists in the pinned space.
2. `UNDERDETERMINED_IN_PINNED_SPACE`: Documentary text exists addressing the parameter, but admits multiple conflicting interpretations without a tie-breaking rule.
3. `NOT_FOUND_IN_PINNED_SPACE`: No specification resolving the parameter was identified within the pinned search space.

### Parameter Definitions

#### P1: Current Sign Polarity
- **Schema Gate:** `APPLICABLE` if current is signed in raw time-series data or summary tables.
- **Evaluation Question:** Does positive current denote charge and negative discharge, or vice-versa?

#### P2: Zero-Code Semantics & Measurement Resolution
- **Schema Gate:** `APPLICABLE` if numerical zeros appear in current, voltage, or capacity columns.
- **Evaluation Question:** Are zero values defined as measured quantities within precision bounds, or do they encode absent/non-applicable steps or sensor nulls?

#### P3: Capacity Representation & Counter Resets
- **Schema Gate:** `APPLICABLE` if capacity or energy columns are reported.
- **Evaluation Question:** Are capacity fields incremental per step/cycle, strictly monotonic cumulative lifetime counters, or multi-step aggregates? When and how do counters reset to zero?

#### P4: Temporal-Support Semantics (B-5)
- **Schema Gate:** `APPLICABLE` to any timestamped export or summary table.
- **Evaluation Question:** What does a recorded timestamp temporally represent (interval start, interval end, midpoint, or instantaneous discrete sample)? Where interval bounds $[t_a, t_b]$ are reported, are boundary points inclusive, exclusive, or half-open, and can adjacent rows share samples?

#### P5: Logging Cadence & Operation Coverage
- **Schema Gate:** `APPLICABLE` to all time-series exports.
- **Evaluation Question:** What rules govern logging rate (fixed interval $\Delta t$, $dV$/$dI$ threshold triggers, or event-driven transitions)? How is complete temporal coverage of an operation verified?

#### P6: Time-Series to Cycle-Summary Mapping
- **Schema Gate:** `APPLICABLE` if exports are partitioned into separate summary and time-series files where index identifiers can repeat.
- **Evaluation Question:** What documented key or rule links a given time-series segment to its exact corresponding cycle-summary record when cycle indices repeat?

---

## 3. Pinned Search Space Hierarchy & Stopping Rule (B-8)

For each audited deposit, the documentary search is strictly partitioned into three hierarchical tiers:

1. **Tier 1 (Deposit Repository & Landing Assets):**
   - Repository landing page, direct dataset `README`, `metadata.json`, data dictionaries, and codebooks stored directly with the deposit.
2. **Tier 2 (Linked Literature & External Frame Binding) (B-8):**
   - Peer-reviewed publications bound to the sampled dataset row by the canonical sampling frame (the `Paper Ref` field in dos Reis et al. Table 2) **AND/OR** explicitly linked by DOI/URL in Tier 1 assets, including published Supplementary Information.
3. **Tier 3 (Equipment Specifications Explicitly Referenced):**
   - Manufacturer hardware/software manuals (e.g., Arbin, Maccor, BioLogic) *strictly and only if* explicitly referenced by Tier 1 or Tier 2 as defining the exported column conventions.

### Pinned Stopping Rule
The search is exhausted once Tier 1, Tier 2, and explicitly referenced Tier 3 items have been audited. Free-form web searching, searching unreferenced user forums, consulting unlinked third-party scripts, or inspecting post-publication repositories is strictly prohibited.

---

## 4. Uniform Depositor Correspondence Protocol

To ensure parity between the calibration case (Sandia) and confirmatory deposits, identical correspondence rules apply across all evaluated cases:

1. **Standardized Inquiry Template:** Each evaluated deposit receives an inquiry containing the identical verbatim text of the six export-semantics questions, addressed to the official depositor contact or corresponding author identified in Tier 1/2.
2. **Uniform Response Cutoff:** Exactly **14 calendar days** (`sent_at + 14 days`), harmonized with the window established for Sandia.
3. **Two-Dimensional Evaluation Output:**
   - **Dimension A (Public Pinned-Space Status):** `RESOLVED`, `UNDERDETERMINED`, or `NOT_FOUND_IN_PINNED_SPACE`.
   - **Dimension B (Depositor Response Status):**
     - `WAITING_EXTERNAL` (during the 14-day window)
     - `NO_DEPOSITOR_RESPONSE` (recorded via explicit Operator commit after cutoff)
     - `PARTIAL_RESPONSE` (itemized resolution of a subset of parameters)
     - `FULL_RESPONSE` (authoritative documentary resolution of all applicable parameters)

---

## 5. Instrument Calibration vs. Empirical Control (B-3)

To ensure methodological validity without circular reasoning, calibration is strictly separated from empirical control:

### A. Instrument Calibration Feasibility Test (`CALIBRATION_POSITIVE`)
- **Subject:** Chung et al. (2021) (`CALIBRATION_POSITIVE`).
- **Function:** Demonstrates that the instrument is capable of registering `RESOLVED_IN_PINNED_SPACE` on a known-good deposit with explicit definitions.
- **Failure Threshold (`INSTRUMENT_INVALID`):** If the instrument fails to register `RESOLVED_IN_PINNED_SPACE` for the pre-asserted explicit parameters (P1, P3, P5) on Chung (2021), the instrument logic is broken, and execution is aborted as `INSTRUMENT_INVALID`.

### B. Confirmatory High-Documentation Control (`CONFIRMATORY_HIGH_DOC_CONTROL`)
- **Subject:** A blind candidate drawn from *Nature Scientific Data* under formal Data Descriptor mandates.
- **Function:** An empirical measurement of whether mandatory data descriptor policies guarantee complete export semantics in practice.
- **Epistemic Invariant:** If this control returns `NOT_FOUND` or `UNDERDETERMINED`, it is an **empirical finding regarding data descriptor boundaries**, and does **NOT** invalidate the instrument.

---

## 6. Intra-Adjudicator Repeatability Test (B-7)

To detect analyst calibration shift and evaluation drift over the lifecycle:
- The first confirmatory target dataset evaluated is assigned a masked, randomized identifier (`MASKED_REPEATABILITY_CTRL`).
- Upon completion of all evaluations, the same analyst re-evaluates `MASKED_REPEATABILITY_CTRL` blind to its original identifier.
- Any discrepancy between the initial and masked adjudication is logged as `INTRA_ADJUDICATOR_DRIFT_DETECTED` in `FAILURES.md`.
