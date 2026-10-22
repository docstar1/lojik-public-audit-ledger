# LojikVantage(TM) | by LojikX(TM) - Public Prediction & Evaluation Archive

**Live page:** <https://docstar1.github.io/lojik-public-audit-ledger/>

This repository is the public, black-box archive of **LojikVantage(TM)**, the private-capital
intelligence platform built by **LojikX(TM)**.

It publishes one page and three CSV files, and nothing else. No source code, no tooling, no
confidential data and no unverified identities.

---

## 1. What is in this repository

| File | What it is |
|------|------------|
| `index.html` | The one-page executive summary: four headline numbers, the monthly archive links, two charts, twelve verified wins and the complete top-10% bucket accounting. |
| `predictions/2026-10_predictions.csv` | The 2026-10 prediction cohort in masked (Option B) form. Every entity name is locked as `[LOCKED UNTIL WIN — ID ...]` until the outcome actually realises, and each row carries only a salted one-way commitment token. There is no score, rank, percentile, sector or feature column. |
| `scorecard/monthly_scorecard_summary.csv` | The monthly evaluation table: our top-decile hits and picks next to the published industry benchmarks, one row per evaluation period, plus the pension alpha and the status of each cohort. |
| `scorecard/verified_sample_wins.csv` | Twelve curated verified wins across the three win tiers. Only three dates and the confirmed real-world outcome are published. |

---

## 2. The monthly cycle

1. On the 22nd of each month the cohort is sealed and the masked prediction file is committed here
   with a GitHub timestamp.
2. At the end of the month the cohort is graded against what actually happened and the scorecard row
   moves from `OPEN` to `CLOSED - VERIFIED`.
3. When a pick is confirmed, its locked identity is released in the private file and the published
   commitment token can be checked against it.

Because every file is a plain CSV committed with a GitHub timestamp, the archive is independently
auditable: clone the repository, or download any file from the live page, and you hold the exact
bytes that were published on that date.

---

## 3. How the numbers were produced

- **Frozen vintages.** Every cohort is ranked on information available at its own cutoff and then
  graded against outcomes realised afterwards.
- **Real disclosed outcomes.** The pension figures are read from official public pension
  partnership disclosures (25 CalSTRS partnerships, FYE June 2024).
- **Complete buckets.** Every pick, every hit and every miss inside the frozen top decile is
  counted. Nothing is filtered after the fact, and each benchmark hit count is implied from the
  published top-decile lift at that cohort base rate.
- **Masked identities.** The published prediction cohort never contains a real entity name, a
  score, a rank, a percentile or a feature column.

---

## 4. Live page

<https://docstar1.github.io/lojik-public-audit-ledger/>

Source of truth: <https://github.com/docstar1/lojik-public-audit-ledger>

*LojikVantage(TM) is a mark of LojikX(TM). This archive is a public audit artefact; it contains no
proprietary source code and no confidential client information.*
