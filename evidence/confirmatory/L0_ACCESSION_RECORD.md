# Level-0 Deposit Accession & Reachability Manifest

- **Governing Freeze Commit:** `4f168f79cd9ea7ba98f7c1449fd0238e7cfa6126`
- **L0 Evaluation Window Started:** `2026-09-12T11:30:14+02:00`
- **Status Accounting:** `FRAME_ATTRITION: 0/3` (All 3 confirmatory units reachable)
- **P1–P6 Semantic Adjudication Started:** `NO` (Strict separation: accession and custody sealing preceding semantic parsing)

---

## Accessioned Confirmatory Units

| Tier / Role | Identifier & Source | Canonical URL | Resolved Landing / Final URL | HTTP Status | L0 Disposition |
|---|---|---|---|---|---|
| `CONFIRMATORY_HIGH_DOC_CONTROL` | `10.1038/s41597-024-03831-x` (Nature Scientific Data) | `https://doi.org/10.1038/s41597-024-03831-x` | `https://www.nature.com/articles/s41597-024-03831-x?error=cookies_not_supported&code=2a4e427c-466a-4485-8dc3-5300b096f094` | `200` | `REACHABLE` |
| `CONFIRMATORY_TARGET_1` | `TRI [71, URL] / [72]` (Toyota Research Institute) | `https://data.matr.io/` | `https://data.matr.io/` | `200` | `REACHABLE_WITH_JS_CLIENT` |
| `CONFIRMATORY_TARGET_2` | `KIT [86, URL] / [8]` (KITopen / RADAR4KIT) | `https://doi.org/10.5445/IR/1000094469` | `https://publikationen.bibliothek.kit.edu/1000094469` | `200` | `REACHABLE` |

---

## Custody & Artifact Verification

Raw HTTP bytes, headers, and metadata are persisted under `evidence/confirmatory/`:
- [`high_doc_control/`](high_doc_control/)
- [`target_1_tri/`](target_1_tri/)
- [`target_2_kit/`](target_2_kit/)

Authoritative checksums for all retrieved landing assets are pinned in [`evidence/confirmatory/SHA256SUMS`](SHA256SUMS).
