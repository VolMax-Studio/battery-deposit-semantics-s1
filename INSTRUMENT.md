# Export Semantics Measurement Instrument (S1)

This instrument specifies the formal measurement protocol, decision boundaries, evidentiary search spaces, and validity criteria for auditing export semantics across public battery degradation datasets.

---

## 1. Grounding: Mathematical Necessity for Reconstruction
The six parameters evaluated by this instrument are not arbitrary bureaucratic conventions. They are the minimal set required to compute Equivalent Full Cycles (EFC) or cumulative throughput deterministically:
$$\text{Throughput} = \int_{t_{\text{start}}}^{t_{\text{end}}} |I(t)|\, dt \quad \text{or} \quad \text{EFC} = \frac{\sum Q_{\text{discharge}}}{Q_{\text{nominal}}}$$
Any missing, contradictory, or underdetermined parameter requires the analyst to introduce unverified numerical assumptions, invalidating reproducible cross-deposit synthesis.

---

## 2. The Six Parameters & Applicability Gates

Prior to documentary adjudication, every parameter is evaluated through an **Applicability Gate** based strictly on the observable physical schema (column names, table layout) of the raw export files:
- `APPLICABLE`: The syntactic schema relies on or contains the structural construct (e.g., column exists, cyclical aggregates present).
- `NOT_APPLICABLE_TO_EXPORT_SCHEMA`: The export architecture does not utilize the construct (e.g., flat, continuous single-column time series without cycle summary or interval bounds).

If `APPLICABLE`, the documentary search space is audited to produce exactly one of three epistemological outcomes:
1. `RESOLVED_IN_PINNED_SPACE`: Explicit, unambiguous documentary specification exists in the pinned space.
2. `UNDERDETERMINED_IN_PINNED_SPACE`: Documentary text exists addressing the parameter, but admits multiple conflicting interpretations without a tie-breaking rule.
3. `NOT_FOUND_IN_PINNED_SPACE`: No specification resolving the parameter was identified within the pinned search space.

### Parameter Definitions

#### P1: Current Sign Polarity
- **Schema Gate:** `APPLICABLE` if current is signed in raw time-series data.
- **Evaluation Question:** Does positive current denote charge and negative discharge, or vice-versa?

#### P2: Zero-Code Semantics & Measurement Resolution
- **Schema Gate:** `APPLICABLE` if numerical zeros appear in current, voltage, or capacity columns.
- **Evaluation Question:** Are zero values defined as measured quantities within precision bounds, or do they encode absent/non-applicable steps or sensor nulls?

#### P3: Capacity Representation & Counter Resets
- **Schema Gate:** `APPLICABLE` if capacity or energy columns are reported.
- **Evaluation Question:** Are capacity fields incremental per step/cycle, strictly monotonic cumulative lifetime counters, or multi-step aggregates? When and how do counters reset to zero?

#### P4: Interval Endpoint Inclusion
- **Schema Gate:** `APPLICABLE` if summary tables report interval start and end timestamps (e.g., `Start_Time`, `End_Time`).
- **Evaluation Question:** Are timestamp boundaries $[t_{\text{start}}, t_{\text{end}}]$ closed, open, or half-open? Can adjacent rows share boundary samples or operations?

#### P5: Logging Cadence & Operation Coverage
- **Schema Gate:** `APPLICABLE` to all time-series exports.
- **Evaluation Question:** What rules govern logging rate (fixed interval $\Delta t$, $dV$/$dI$ threshold triggers, or event-driven transitions)? How is complete temporal coverage of an operation verified?

#### P6: Time-Series to Cycle-Summary Mapping
- **Schema Gate:** `APPLICABLE` if exports are partitioned into separate summary and time-series files where index identifiers can repeat.
- **Evaluation Question:** What documented key or rule links a given time-series segment to its exact corresponding cycle-summary record when cycle indices repeat?

---

## 3. Pinned Search Space Hierarchy & Stopping Rule

For each audited deposit, the documentary search is strictly partitioned into three hierarchical tiers:

1. **Tier 1 (Deposit Repository & Landing Assets):**
   - Repository landing page, direct dataset `README`, `metadata.json`, data dictionaries, and codebooks stored directly with the deposit.
2. **Tier 2 (Linked Peer-Reviewed Literature & Data Descriptors):**
   - Publications or data descriptor articles directly cited by DOI in Tier 1 assets, including published Supplementary Information.
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

## 5. Instrument Validity Rule (`INSTRUMENT_VALIDITY`)

The instrument must be falsifiable and capable of measuring completeness.
- **Minimal Necessary Reconstruction Core:** $\{P1, P3\}$.
- **Validity Invariant:**
  - The blind `CONFIRMATORY_POSITIVE` control must return `RESOLVED_IN_PINNED_SPACE` for $\{P1, P3\}$.
  - For $P4$, it must return either `RESOLVED_IN_PINNED_SPACE` (if schema is segmented) or `NOT_APPLICABLE_TO_EXPORT_SCHEMA` (if schema is flat/continuous).
  - If `CONFIRMATORY_POSITIVE` returns `NOT_FOUND` or `UNDERDETERMINED` for $P1$ or $P3$, the instrument is formally declared **`INSTRUMENT_INVALID`**.
  - Under `INSTRUMENT_INVALID`, evaluation of all target deposits is immediately aborted, and no scientific conclusions regarding target datasets are adjudicated.

---

## 6. Adjudicator Drift Control

To detect analyst calibration shift over the evaluation lifecycle:
- The first confirmatory target dataset evaluated is assigned a masked, randomized identifier (`MASKED_DRIFT_CTRL`).
- Upon completion of all evaluations, the same analyst re-evaluates `MASKED_DRIFT_CTRL` blind to its original identifier.
- Any discrepancy between the initial and masked adjudication is logged as `ADJUDICATOR_DRIFT_DETECTED` in `FAILURES.md`.
