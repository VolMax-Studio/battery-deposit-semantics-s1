# Sampling Frame & Dataset Selection Protocol (S1)

This specification establishes the external sampling frame, eligibility criteria, deterministic hash-ranking algorithm, and positive control pool for instance `battery-deposit-semantics-s1`.

---

## 1. External Denominator & Canonical Sampling Source

To eliminate selection bias, the sampling frame is drawn strictly from an external, peer-reviewed review published prior to the design of this instrument:
- **Article:** Gonçalo dos Reis, Calum Strange, Mohit Yadav, Shawn Li, *Lithium-ion battery data and where to find it*, Energy and AI 5 (2021), 100081.
- **DOI:** `10.1016/j.egyai.2021.100081`
- **Canonical Object:** Table 2 ("Overview of cycle ageing datasets") in the published Version of Record.
- **Sampling Unit:** A unique dataset row in Table 2 (not an institution or research group).

---

## 2. Eligibility Criteria & Filtering Rule

A Table 2 row is deemed eligible for inclusion if and only if all of the following conditions are met:
1. **Ageing Classification:** The entry represents commercial cell cycle-ageing data.
2. **Signal Completeness:** The "Data given" column explicitly includes both voltage ($V$) and current ($I$).
3. **Public Availability Indicator:** A public dataset URL or institutional location is provided.
4. **Mandatory Exclusion:** Any row corresponding to the Sandia commercial cell dataset is strictly excluded, as it serves as the inductive `CALIBRATION_CASE`.

---

## 3. Deterministic Selection Algorithm (Hash-Sort)

To ensure zero discretion in dataset selection, candidate rows are ranked using a deterministic hash function:

### A. Canonical Key Construction
For each eligible Table 2 row:
$$\text{canonical\_key} = \text{lower}(\text{strip}(\text{Location})) \,\|\, \text{"|"} \,\|\, \text{lower}(\text{strip}(\text{Paper Ref})) \,\|\, \text{"|"} \,\|\, \text{lower}(\text{strip}(\text{Cell descriptor}))$$

### B. Selection Score
$$\text{selection\_score} = \text{SHA256}(\text{"battery-deposit-semantics-s1|10.1016/j.egyai.2021.100081|"} \,\|\, \text{canonical\_key})$$

### C. Ranking & Selection
1. All eligible rows are sorted in ascending lexicographical order by `selection_score`.
2. The first two entries become:
   - `CONFIRMATORY_TARGET_1`
   - `CONFIRMATORY_TARGET_2`

### D. Attrition Handling (`FRAME_ATTRITION`)
If a selected repository URL is permanently unreachable at Level-0 verification (404, repository retired, domain defunct):
- It is formally logged as `FRAME_ATTRITION` in `FAILURES.md`.
- The next eligible row in ascending `selection_score` order is selected as the replacement.
- Documentation quality, format complexity, or perceived difficulty of adjudication shall never serve as grounds for dataset replacement.

---

## 4. Positive Control Protocol

### A. Calibration Positive (`CALIBRATION_POSITIVE`)
- **Dataset:** Chung et al., *Scientific Data* 8, 165 (2021), DOI: `10.1038/s41597-021-00954-3`.
- **Function:** Serves as a known-good reference demonstrating instrument feasibility for explicitly defined export semantics (P1, P3, P5).

### B. Confirmatory Positive (`CONFIRMATORY_POSITIVE`)
- **Pool Definition:** Articles published in *Nature Scientific Data* under battery degradation / cycling subjects that mandate formal Data Descriptors, snapshot prior to freeze.
- **Strict Exclusion:** Chung (2021) is barred from selection.
- **Blindness Invariant:** Selection occurs via deterministic hash ranking over published DOIs post-freeze. The data files, READMEs, and technical appendices of the chosen candidate shall remain unopened until the execution phase.

---

## 5. Sample Size & Scope of Adjudication
- **Evaluated Set:** Exactly $n = 4$ datasets:
  1. `CALIBRATION_POSITIVE` ($1$)
  2. `CONFIRMATORY_POSITIVE` ($1$)
  3. `CONFIRMATORY_TARGET_1` ($1$)
  4. `CONFIRMATORY_TARGET_2` ($1$)
- **Scope Limit:** Findings apply strictly to the evaluated sample under the preregistered frame and search boundaries. This study does not generalize to a global claim regarding all battery data repositories in existence.
