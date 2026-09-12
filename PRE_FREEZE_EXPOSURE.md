# Pre-Freeze Exposure & Prior Knowledge Audit

This document preregisters all prior exposure, preliminary observations, analyst claims, and model errors known prior to the formal freeze of instance `battery-deposit-semantics-s1`.

---

## 1. Prior Cases & Asymmetric Knowledge Disclosure

### A. Sandia Degradation Dataset (`CALIBRATION_CASE` / Observed Case)
- **Status:** Explicitly classified as `CALIBRATION_CASE`. It is **NOT** a confirmatory test.
- **Prior Knowledge:** The six export-semantics questions were derived inductively during preliminary audit passes on this dataset.
- **Observed Prior Finding:** All six parameters were observed as unestablished (`0/6`) within the preliminary documentary search space.
- **Correspondence State:** An inquiry was sent on `2026-09-09T23:24:04+02:00` to `info@batteryarchive.org`; response cutoff is `2026-09-23T23:24:04+02:00` under portfolio instance `sandia-battery-degradation-s1`.

### B. Chung et al. (2021) (`CALIBRATION_POSITIVE` / Known Positive Case)
- **Citation:** Hsien-Ching Chung, *Charge and discharge profiles of repurposed LiFePO4 batteries based on the UL 1974 standard*, Scientific Data 8, 165 (2021), DOI: `10.1038/s41597-021-00954-3`; machine-accessible metadata DOI: `10.6084/m9.figshare.14495604`.
- **Status:** Explicitly classified as `CALIBRATION_POSITIVE`. It is **NOT** a blind confirmatory test.
- **Prior Claims Asserted Before Freeze:**
  - **P1 (Current Polarity):** Pre-asserted by analyst (Sol) as explicitly defined in article text.
  - **P3 (Capacity & Reset):** Pre-asserted by analyst (Sol) as explicitly defined (distinguishing instantaneous from accumulated quantities, capacity/energy reset to zero at step onset).
  - **P5 (Sampling Cadence):** Pre-asserted by analyst (Sol) as explicitly defined (10-second sampling cadence in CSV columns).
- **Mandatory Exclusion:** Chung (2021) is **strictly barred** from inclusion in the candidate pool for `CONFIRMATORY_POSITIVE`.

### C. dos Reis et al. (2021) (`SAMPLING_FRAME_ARTICLE`)
- **Citation:** Gonçalo dos Reis, Calum Strange, Mohit Yadav, Shawn Li, *Lithium-ion battery data and where to find it*, Energy and AI 5 (2021), 100081, DOI: `10.1016/j.egyai.2021.100081`.
- **Prior Knowledge:** Article metadata and Table 2 ("Overview of cycle ageing datasets") have been inspected to establish the sampling frame denominator.
- **Strict Boundary:** **Zero** dataset URLs, repository links, data files, or deposit-specific documentation from Table 2 entries have been accessed, followed, or evaluated prior to freeze.

---

## 2. Model Error Log Captured Pre-Freeze

### F-PF-01: Hallucinated DOI Interception
- **Detected By:** Sol (analyst) & External Reviewer.
- **Erroneous Citation Emitted by Model:** `10.1016/j.est.2021.102250` attributed to *Journal of Energy Storage* / *dos Reis et al.*.
- **Factual Correction:** The true publication is *Energy and AI*, Vol. 5, Article 100081 (2021), DOI: `10.1016/j.egyai.2021.100081`.
- **Epistemic Disposition:** Captured in pre-freeze audit; verified against the publisher record (Elsevier / ScienceDirect) before inclusion in any repository artifact.
