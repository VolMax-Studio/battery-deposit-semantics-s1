# battery-deposit-semantics-s1

**Preregistered, artifact-first audit of export semantics in public lithium-ion battery degradation deposits.**

> **Terminal state:** `INSTRUMENT_INVALID`  
> **Terminal commit:** `8812111d77e3526ec07a6d613fa4e82594496b9d`  
> **Governing preregistration freeze:** `4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126`  
> **Bound candidate:** `b8aa8a71f2bfa76ebb298e18b6803428462757c6`

## What this instance tested

S1 asked whether public battery-degradation deposits and their pinned public documentation unambiguously define the export semantics needed for reproducible throughput / Equivalent Full Cycle (EFC) reconstruction, or whether critical conventions remain unresolved without off-artifact depositor correspondence.

The measurement instrument was frozen before verdict-bearing execution. It evaluated six export-semantics parameters under explicit applicability gates and a bounded Tier 1–3 documentary search space. Missing or ambiguous semantics were not silently repaired from analyst intuition, third-party scripts, or unrestricted web search.

The central design principle was simple:

```text
claim → admissible public artifacts → frozen test → literal execution evidence → bounded outcome
```

## Why S1 terminated

S1 included a non-blind internal calibration case, Chung et al. (2021), DOI `10.1038/s41597-021-00954-3`. The frozen validity rule required the calibration instrument to register `RESOLVED_IN_PINNED_SPACE` for all three pre-asserted parameters: **P1, P3, and P5**.

Execution established:

- **P1 — Current Sign Polarity:** resolved in pinned space.
- **P3 — Capacity Representation & Counter Resets:** resolved in pinned space.
- **P5 — Logging Cadence & Operation Coverage:** only partially resolved under the frozen compound definition.
  - logging cadence was explicitly documented (`Δt = 10 s`);
  - an explicit documentary protocol for verifying complete temporal operation coverage was not identified in the pinned space.

The frozen gate required **3/3**. The calibration case therefore achieved **2/3**, which mechanically triggered:

```text
INSTRUMENT_INVALID
```

No post-hoc relaxation, parameter split, or validity-rule rewrite was permitted inside S1.

## What `INSTRUMENT_INVALID` means

`INSTRUMENT_INVALID` is a terminal statement about the **frozen S1 validity architecture**. It does **not** mean that:

- the underlying battery datasets are invalid;
- the publishers or repositories failed generally;
- P1, P3, or the cadence component of P5 are meaningless;
- public battery data cannot support reproducible analysis;
- the confirmatory deposits were tested and failed.

The instrument invalidated itself because its preregistered calibration criterion did not hold as written.

## Confirmatory sample: no semantic verdicts

S1 froze three confirmatory observation units:

1. `CONFIRMATORY_HIGH_DOC_CONTROL` — DOI `10.1038/s41597-024-03831-x`
2. `CONFIRMATORY_TARGET_1` — dos Reis Table 2: `TRI [71, URL] / [72]`
3. `CONFIRMATORY_TARGET_2` — dos Reis Table 2: `KIT [86, URL] / [8]`

A Level-0 accession step was performed before calibration completion and is preserved in the execution history. However, **no valid P1–P6 confirmatory semantic adjudication was performed**.

Accordingly:

```text
confirmatory_high_doc_control_status: NOT_ADJUDICATED
confirmatory_targets_status:          NOT_ADJUDICATED
verdict-bearing confirmatory results: NONE
```

The confirmatory deposits must not be described as Verified, Not Verified, Not Demonstrated, or semantically incomplete on the basis of S1.

## Execution history

| Stage | Commit | Meaning |
|---|---|---|
| Candidate preregistration | `b8aa8a71f2bfa76ebb298e18b6803428462757c6` | Accepted candidate specification |
| Freeze ratification | `4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126` | Governing frozen protocol |
| Confirmatory L0 accession | `fbe609d75bbc0b50e2c7b8c586193f3d63120322` | Reachability/custody only; no semantic adjudication |
| Calibration v1 | `c2d7ecf87a7d6b247bf8013f37a41be92ac97834` | Flawed execution dossier; retained append-only |
| Calibration v2 / custody remediation | `34d4afa6259f9f1c4f062ca34bf431887f508098` | Authentic raw-schema custody and corrected evidence |
| Terminal closure | `8812111d77e3526ec07a6d613fa4e82594496b9d` | `INSTRUMENT_INVALID`; confirmatory execution halted |

## Failure history is part of the evidence

`FAILURES.md` is append-only and records `F-001` through `F-007`, including intercepted citation/provenance defects, sampling-unit duplication, execution sequencing inversion, calibration transcription errors, custody remediation, P5 overclaim detection, and the terminal validity failure.

The project intentionally preserves failed intermediate commits rather than rewriting history. Later corrections do not erase earlier defects.

## Non-verdict-bearing trace

S1 produced one potentially important **exploratory trace**: in the exposed Chung calibration case, the pinned Scientific Data documentation explicitly specified logging cadence but did not provide an explicit protocol meeting S1's frozen requirement for verification of complete temporal operation coverage.

Because Chung was a non-blind calibration case and S1 terminated `INSTRUMENT_INVALID`, this observation is **not an S1 confirmatory empirical finding** and must not be promoted to one.

## Repository map

- `PREREGISTRATION.md` — frozen research question, invariants, calibration rule, and prohibitions
- `INSTRUMENT.md` — six-parameter measurement instrument, applicability gates, search-space rules, and validity criteria
- `SAMPLING_FRAME.md` — deterministic sampling frame and observation-unit rules
- `PRE_FREEZE_EXPOSURE.md` — known pre-freeze exposures and contamination disclosures
- `FAILURES.md` — append-only defect and deviation history
- `STATUS.md` — authoritative terminal state
- `artifacts/` — frozen sampling-frame artifacts and checksums
- `evidence/calibration/` — calibration custody and execution evidence
- `evidence/confirmatory/` — Level-0 accession history only

## Reproducibility boundary

For historical reconstruction of S1, use the governing freeze commit:

```text
4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126
```

For the final terminal state, use:

```text
8812111d77e3526ec07a6d613fa4e82594496b9d
```

The repository should be read as an immutable audit trail: preregistration first, execution second, failures preserved, and terminal state determined by the frozen rules rather than by desired outcome.

## Successor work

Any successor instance is a **separate project**. S1 does not contain a public S2 design or a successor decision-rule specification. Because S1 construction and review materially exposed the failure boundary, successor methodology must disclose those exposures and satisfy the project's independence rules before prospective execution.
