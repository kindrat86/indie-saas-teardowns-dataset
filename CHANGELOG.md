# Changelog

All notable changes to the **Indie SaaS Teardowns Dataset** are recorded
here, in reverse chronological order. The canonical version lives at
https://unlocksaas.com/dataset; this file is auto-prepended by the weekly
mirror workflow on every refresh that actually changes content.

Versioning is SemVer. See [README.md § Versioning](./README.md#versioning).

---

## 1.0.0 – 2026-05-25 (weekly refresh)

Canonical lastVerified: `2026-05-18` · Total rows: **159**

"| Table | Before | After | Δ |\n|---|---:|---:|---:|\n| funnel_teardowns | 33 | 33 | 0 |\n| pricing_teardowns | 31 | 31 | 0 |\n| comparisons | 61 | 61 | 0 |\n| alternatives | 21 | 21 | 0 |\n| categories | 13 | 13 | 0 |\n| total_rows | 159 | 159 | 0 |"

Pulled from https://unlocksaas.com/dataset by the weekly mirror workflow.

---


## 1.0.0 – 2026-05-18 (initial public mirror)

### Added

- Initial public GitHub mirror seeded from production at
  https://unlocksaas.com/dataset.
- Five tables: 33 funnel teardowns, 31 pricing teardowns, 61 head-to-head
  comparisons, 21 named-competitor alternatives, 13 canonical category
  buckets. Total: **159 rows**.
- Universal flat CSV (`data/indie-saas-teardowns.csv`, 14 columns,
  `record_type` discriminator).
- Per-table CSVs with table-specific column shapes
  (`data/tables/*.csv`).
- Self-describing JSON bundle (`data/indie-saas-teardowns.json`) with
  schema, citation metadata, license, BibTeX, and row counts.
- Persistent DOI: https://doi.org/10.5281/zenodo.20315741.
- CC-BY-4.0 license file with required attribution string.
- GitHub-rendered citation widget via `CITATION.cff`.

### Refresh policy

The mirror refreshes weekly on Monday at 06:00 UTC. PRs only land when
content has actually changed. Silent weeks are normal.
