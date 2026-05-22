# Indie SaaS Teardowns Dataset

> An open editorial dataset of indie SaaS marketing analysis: funnel teardowns, pricing teardowns, head-to-head comparisons, named-competitor alternatives, and canonical category buckets. Every row is independently verifiable against a dated, attributed editorial source page on unlocksaas.com.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20315741.svg)](https://doi.org/10.5281/zenodo.20315741)
[![Canonical](https://img.shields.io/badge/canonical-unlocksaas.com%2Fdataset-0a0a0a)](https://unlocksaas.com/dataset)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://unlocksaas.com/dataset)
[![Rows](https://img.shields.io/badge/rows-159-success.svg)](https://unlocksaas.com/dataset)

**Canonical home:** https://unlocksaas.com/dataset
**Persistent DOI:** https://doi.org/10.5281/zenodo.20315741
**License:** CC-BY-4.0 (attribution required, commercial re-use allowed, no share-alike)
**Publisher:** [Unlock SaaS](https://unlocksaas.com)
**Refresh cadence:** weekly auto-PR from production on Monday 06:00 UTC

This repository is a **public GitHub mirror** of the dataset published at https://unlocksaas.com/dataset. The site is the source of truth; this mirror is refreshed every Monday by an automated workflow that fetches the canonical files and opens a pull request when the row counts, content, or schema have changed.

---

## Why this dataset exists

Most indie SaaS marketing analysis lives inside paid courses, locked Notion docs, or behind sign-up walls. The editorial moat at unlocksaas.com is the opposite: every funnel teardown, pricing teardown, head-to-head comparison, and named-competitor alternative is published as a public HTML page, dated with `lastVerified`, and reviewed against an editorial policy on every quarterly cycle.

This dataset is a re-projection of those pages into shapes researchers, indie founders, newsletter writers, and academics can re-use without scraping HTML: a self-describing JSON bundle, a universal flat CSV, and five per-table CSVs with table-specific columns. Brunson's Hook / Story / Offer framework and Value Ladder are the analytical lens; the data is the receipts.

---

## What's in the box

| Table | Rows | What it contains |
|---|---:|---|
| Funnel teardowns | 33 | Hook / Story / Offer pattern analysis of indie SaaS homepages and sales funnels. Brunson lens, what's working, what to adapt, what to avoid, FAQ. |
| Pricing teardowns | 31 | Pricing model, payment frequency, free-trial behavior, anchor pattern, upgrade trigger, Brunson stack + value ladder analysis. |
| Head-to-head comparisons | 61 | Symmetric "A vs B" pages with best-for fields, pick-A-if / pick-B-if lists, dimension count, honest take, indie-founder verdict. |
| Alternatives | 21 | Honest named-competitor pages. What-it-is / what-it-is-not, audience fit, honest verdict, capability count. |
| Categories | 13 | Canonical category buckets that group teardowns, comparisons, and alternatives into roundup pages. |
| **Total** | **159** | |

Each row carries a stable `slug`, a dated `lastVerified` ISO field, and a `canonical_url` that resolves to the source page on unlocksaas.com.

---

## Files in this repository

```
data/
├── indie-saas-teardowns.json       # Full bundle with schema, citation, counts, all tables
├── indie-saas-teardowns.csv        # Universal flat CSV (14 columns, record_type discriminator)
└── tables/
    ├── funnel-teardowns.csv        # 27 columns: hook/story/offer + Brunson lens
    ├── pricing-teardowns.csv       # 29 columns: pricing model + anchor + upgrade trigger
    ├── comparisons.csv             # 22 columns: pick-A-if, pick-B-if, indie-founder pick
    ├── alternatives.csv            # 17 columns: whatItIs / whatItIsNot + honest verdict
    └── categories.csv              # 8 columns: matchers, intent paragraphs
```

Both CSV shapes are intentional. The universal CSV is for indexers, leaderboards, and one-line `pd.read_csv()` workflows. The per-table CSVs are for downstream analyses that respect each record type's actual schema.

The full JSON bundle is self-describing: it includes schema descriptions, citation metadata, the BibTeX entry, license attribution, row counts, and `lastVerified` / `nextReview` dates so a downstream consumer that pops it open in `jq` immediately understands what's in front of them.

---

## How to use it

### Python (pandas)

```python
import pandas as pd

# Universal flat CSV (all five tables, discriminated by record_type)
df = pd.read_csv("https://unlocksaas.com/dataset/indie-saas-teardowns.csv")

# Just the funnel teardowns with full schema
funnels = pd.read_csv("https://unlocksaas.com/dataset/tables/funnel-teardowns.csv")
print(funnels[["display_name", "hook_pattern", "offer_pattern", "last_verified"]].head())
```

### JavaScript / TypeScript

```ts
const bundle = await fetch(
  "https://unlocksaas.com/dataset/indie-saas-teardowns.json"
).then(r => r.json());

console.log(bundle.counts);
// { funnel_teardowns: 33, pricing_teardowns: 31, comparisons: 61, ... }
```

### Hugging Face Datasets

```python
from datasets import load_dataset

ds = load_dataset("unlocksaas/indie-saas-teardowns")
```
*(Available once the operator activates the HF cross-listing; see `Mirrors` below.)*

### Shell / jq

```bash
curl -sL https://unlocksaas.com/dataset/indie-saas-teardowns.json \
  | jq '.tables.funnel_teardowns | map({slug, displayName, lastVerified})'
```

---

## License

This dataset is licensed under [Creative Commons Attribution 4.0 International (CC-BY-4.0)](https://creativecommons.org/licenses/by/4.0/). Re-use is unrestricted (including commercial). The only obligation is attribution.

**Required attribution string:**

> Source: Unlock SaaS — Indie SaaS Teardowns Dataset (https://unlocksaas.com/dataset). Licensed under CC-BY-4.0.

If you cite the dataset in academic work, please use the persistent DOI: [10.5281/zenodo.20315741](https://doi.org/10.5281/zenodo.20315741).

See [`LICENSE`](./LICENSE) for the full Creative Commons text.

---

## Citation

### Plain text (APA-style)

> Maryan (2026-05-18). *Indie SaaS Teardowns Dataset*, v1.0.0. Unlock SaaS. https://unlocksaas.com/dataset. CC-BY-4.0. DOI: https://doi.org/10.5281/zenodo.20315741.

### BibTeX

```bibtex
@misc{unlocksaas_indie_saas_teardowns_1_0_0,
  author       = {Maryan},
  title        = {{Indie SaaS Teardowns Dataset}},
  howpublished = {\url{https://unlocksaas.com/dataset}},
  year         = {2026},
  doi          = {10.5281/zenodo.20315741},
  note         = {Version 1.0.0. Licensed under CC-BY-4.0.}
}
```

### Machine-readable

The repository ships a [`CITATION.cff`](./CITATION.cff) file that GitHub renders as the right-sidebar "Cite this repository" widget. Five other formats (MLA, Chicago, RIS, CSL-JSON) are available on the [canonical landing page](https://unlocksaas.com/dataset).

---

## Mirrors

The same artifact is published in multiple registered catalogs so a consumer can pick the surface that fits their pipeline.

| Catalog | Status | URL |
|---|---|---|
| Canonical (Unlock SaaS) | ✓ Live | https://unlocksaas.com/dataset |
| Zenodo (DOI) | ✓ Live | https://doi.org/10.5281/zenodo.20315741 |
| GitHub (this mirror) | ✓ Live | https://github.com/kindrat86/indie-saas-teardowns-dataset |
| Hugging Face Datasets | Pending operator activation | https://huggingface.co/datasets/unlocksaas/indie-saas-teardowns |
| Kaggle Datasets | Reserved | — |
| OSF.io | Reserved | — |

---

## Refresh cadence and how PRs land

A GitHub Actions workflow in the main UnlockSaaS repository runs every Monday at 06:00 UTC. The workflow:

1. Fetches the seven canonical files from https://unlocksaas.com/dataset.
2. Compares row counts and content hashes against the previous mirror state.
3. If anything changed, opens a pull request on this repo with the deltas summarized in the body and a new entry prepended to [`CHANGELOG.md`](./CHANGELOG.md).
4. If nothing changed, the workflow exits cleanly and opens no PR. The mirror stays quiet on weeks the canonical dataset is stable.

The PR is opened by `unlocksaas-bot` (a workflow user). Merging it lands the refresh; closing it skips the week. Manual refresh: `workflow_dispatch` from the main repo's Actions tab.

---

## Reporting corrections

The Brunson Hard-Rule editorial standard at unlocksaas.com requires every row to be independently verifiable against the source page it represents. If you find a row that looks wrong:

1. **Open an issue on this repo** using the "Data correction" template. Include the row's `slug`, the field you believe is wrong, and a public source that disagrees.
2. **Or file directly on the canonical page** at https://unlocksaas.com/dataset/corrections — corrections logged there propagate to the next weekly refresh.

Every correction is logged in the public corrections section of the [editorial policy](https://unlocksaas.com/editorial-policy). Silent rewrites of historical claims are forbidden.

---

## Methodology

This dataset is an **editorial corpus**, not a scrape. Every row is a re-projection of a published page authored by the founder, dated, and reviewed against the public editorial policy before publication. No inferred metrics, no fabricated review counts, no traffic estimates.

See [`docs/methodology.md`](./docs/methodology.md) for the full method, or the canonical [editorial policy](https://unlocksaas.com/editorial-policy).

---

## Related resources from Unlock SaaS

- 📊 [Canonical dataset landing](https://unlocksaas.com/dataset) – conversion recipes for Parquet / Arrow / Excel, more citation formats, schema documentation.
- 🧠 [Brunson glossary](https://unlocksaas.com/glossary) – defined terms for every concept used in the editorial lens.
- 📈 [State of UnlockSaaS](https://unlocksaas.com/state-of-saas) – annual snapshot report with dataset citations.
- 🎙️ [Dataset changelog podcast](https://unlocksaas.com/podcast) – every version bump, new table, and cross-catalog activation as a dated episode.
- 🔌 [MCP server](https://unlocksaas.com/mcp) – AI-agent access to the dataset via Model Context Protocol.
- 📚 [Pricing teardowns](https://unlocksaas.com/pricing-teardown) · [Funnel teardowns](https://unlocksaas.com/funnel-teardown) · [Comparisons](https://unlocksaas.com/vs) · [Alternatives](https://unlocksaas.com/alternatives-to) – the source pages this dataset re-projects.

---

## Versioning

Dataset version is SemVer.

- **Patch** (`1.0.x`) – additive changes: new catalog entries, new optional columns, corrections to existing rows.
- **Minor** (`1.x.0`) – renames, type changes, or new tables. A migration note ships in the changelog.
- **Major** (`x.0.0`) – removed columns or removed record types. Consumers should branch on the major.

Current version: **1.0.0** (since 2026-05-18).

---

*This README is auto-refreshed by the weekly mirror workflow. Do not edit it directly — the canonical content lives at https://unlocksaas.com/dataset and propagates here on the next Monday refresh.*
