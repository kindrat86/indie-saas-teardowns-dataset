# Methodology

> A snapshot of how the **Indie SaaS Teardowns Dataset** is produced.
> The canonical, dated, corrections-tracked version lives at
> https://unlocksaas.com/editorial-policy and propagates here on every
> weekly refresh.

## One sentence

Every row in this dataset is a re-projection of a published HTML page on
https://unlocksaas.com that was authored by the founder, dated, and reviewed
against a public editorial policy before publication.

## What "editorial corpus" means

This is **not** a scrape. Three properties separate an editorial corpus
from a scraped dataset:

1. **Authored source.** Every page this dataset re-projects was written by a
   named human author (the founder), not assembled from third-party text.
2. **Dated.** Every page carries an ISO `lastVerified` field. The dataset
   carries the same field through; we do not bump it at dataset build time.
3. **Corrections-tracked.** The editorial policy at unlocksaas.com publishes
   a corrections log. Silent rewrites of historical claims are forbidden.

## What is NOT in this dataset

The Brunson Hard-Rule editorial standard forbids fabricating any of the
following. None of these appear in the rows:

- **Fabricated review counts.** No "4.7 stars (2,341 reviews)" claims unless
  the dataset directly mirrors a public review platform that publishes the
  number. As of v1.0.0, no row carries review counts.
- **Inferred user counts.** No "10,000+ founders use this" without a public,
  verifiable source. No user counts appear.
- **Traffic estimates.** No SimilarWeb / Ahrefs / SEMrush-style traffic
  estimates. The dataset is editorial analysis, not a traffic atlas.
- **Aspirational pricing.** Approximate prices are flagged "approximate" in
  the JSON. The CSV column names mirror the JSON property names so the
  hedge survives the projection.

## What IS in this dataset

For each of the five tables, the row schema mirrors the source catalog's
TypeScript type:

### Funnel teardowns (33 rows)

Hook / Story / Offer pattern analysis through Russell Brunson's framework.
Columns include: hook pattern + analysis, story pattern + analysis, offer
pattern + analysis, what's working, what to adapt, what to avoid, Brunson
lens (hook / story / offer / value ladder tier), tags, FAQ.

### Pricing teardowns (31 rows)

Pricing model, payment frequency, free-trial behavior, tier count, anchor
pattern + analysis, upgrade-trigger pattern + analysis, Brunson lens (stack,
value ladder, decoy/anchor, payment mechanics).

### Head-to-head comparisons (61 rows)

Symmetric "A vs B" pages with: best-for fields per side, pick-A-if /
pick-B-if lists, dimension count, honest take, indie-founder verdict.

### Alternatives (21 rows)

Honest named-competitor pages: what-it-is / what-it-is-not, audience fit
(who-for / who-not-for), honest verdict, pricing note, capability count.

### Categories (13 rows)

Canonical buckets used to group teardowns into roundup pages: display name,
intent paragraph (AEO target), matcher strings (used in routing).

## How a row gets into the dataset

1. **Author writes the source page.** A teardown, comparison, alternative,
   or category bucket lives in a TypeScript catalog under
   `app/src/lib/*.ts` in the source repository. The catalog row carries
   `slug`, `lastVerified`, `tags`, and table-specific structured fields.
2. **Editorial review.** Every catalog row is reviewed against the
   editorial policy before publication. The review checks: no fabricated
   metrics, dated `lastVerified`, attribution links, honest verdict.
3. **Catalog change deploys to production.** The HTML page at the canonical
   URL (`/funnel-teardown/<slug>`, `/pricing-teardown/<slug>`,
   `/vs/<slug>`, `/alternatives-to/<slug>`, `/category/<slug>`) updates.
4. **Dataset rebuilds at deploy time.** The JSON bundle and CSV projections
   are recomputed from the same TypeScript constants the HTML pages render
   from. The dataset cannot drift from the HTML.
5. **Weekly mirror.** This GitHub mirror's workflow fetches the canonical
   files on Monday 06:00 UTC. If anything changed since last week, a PR
   opens here with the deltas.

## How corrections work

Two paths:

1. **Open an issue on this repo** using the "Data correction" template.
   The maintainer reviews against the public source you cite. If the
   correction is accepted, the source catalog updates in the main
   repository, the canonical HTML page updates on the next deploy, and the
   weekly mirror PR carries the change here.
2. **File on the canonical site** at https://unlocksaas.com/dataset/corrections.
   Same flow, fewer hops.

Every accepted correction is logged in the public corrections section of
the [editorial policy](https://unlocksaas.com/editorial-policy). The log
includes: date submitted, row affected, field corrected, prior value, new
value, and the source citation used to settle the correction.

## Versioning

SemVer:

- **Patch** (`1.0.x`) – additive changes: new catalog entries, corrections
  to existing rows, new optional columns.
- **Minor** (`1.x.0`) – renames, type changes, or new tables. A migration
  note ships in the changelog.
- **Major** (`x.0.0`) – removed columns or removed record types. Consumers
  should branch on the major.

## Pointers

- [Canonical editorial policy](https://unlocksaas.com/editorial-policy) –
  the source of truth; this file is a snapshot.
- [Brunson glossary](https://unlocksaas.com/glossary) – defined terms for
  every concept used in the editorial lens.
- [Canonical dataset landing](https://unlocksaas.com/dataset) – schema
  documentation, conversion recipes, additional citation formats.
