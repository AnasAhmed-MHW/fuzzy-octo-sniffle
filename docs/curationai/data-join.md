---
title: Curation AI Data Join
parent: CurationAI
last_modified_date: 2026-04-29 12:00
---

# `bronze_curationai` — Data Pipeline Documentation

## Overview

This pipeline builds a domain-level quality scoring table by joining four data sources, scoring each domain across key performance dimensions, and writing the result to `hive_metastore.default.bronze_curationai`. The table is also synced to DynamoDB for downstream consumption.

---

## Data Sources

### 1. `df_attention`
**Source:** `hive_metastore._global.bronze_lumen_attention`  
**Filter:** `measured_impressions > 50`  
**Aggregation:** grouped by `domain`

| Column | Type | Description |
|---|---|---|
| `domain` | string | Website domain (join key) |
| `impressions` | double | Average measured impressions per domain |
| `attention` | double | Time-in-view in ms per 1,000 impressions `(1000 × sum(view_time_secs)) / sum(impressions)` |

**Example rows:**

| domain | impressions | attention |
|---|---|---|
| echo-news.co.uk | 197.39 | 888.95 |
| moneyprodigy.com | 69.00 | 558.81 |

---

### 2. `df_ethical`
**Source:** `EMI - Raw.csv` (external file — `/Volumes/raw/global/external_files/`)

| Column | Type | Description |
|---|---|---|
| `domain` | string | Website domain (join key) |
| `ethical` | double | EMI ethical score (higher = more ethical) |

**Example rows:**

| domain | ethical |
|---|---|
| scientificamerican.com | 86 |

---

### 3. `df_speed`
**Source:** `hive_metastore.default.bronze_page_speed`  
**Aggregation:** `AVG(performance_score)` grouped by URL, then URL is cleaned to bare domain

| Column | Type | Description |
|---|---|---|
| `domain` | string | Cleaned domain (strips `https://`, `www.`, trailing `/`) |
| `speed` | double | Avg Lighthouse performance score (0–1 scale) |

**Example rows:**

| domain | speed |
|---|---|
| duluxdecoratorcentre.co.uk | 0.2923 |
| moneyprodigy.com | 0.6227 |

---

### 4. `df_performance`
**Source:** *(to be integrated)*

| Column | Type | Description |
|---|---|---|
| `domain` | string | Website domain (join key) |
| `cpm` | double | Cost per mille — **lower is better** |

**Example rows:**

| domain | cpm |
|---|---|
| duluxdecoratorcentre.co.uk | 1.29 |

---

### 5. `df_categories`
**Source:** `hive_metastore.default.domain_categories`

| Column | Type | Description |
|---|---|---|
| `domain` | string | Website domain (join key) |
| `website_category` | string | IAB-style category label |

**Example rows:**

| domain | website_category |
|---|---|
| moneyprodigy.com | Finance & Business |

---

### 6. `df_page_level`
**Source:** `hive_metastore.default.bronze_contextual_arc_all`  
**Deduplication:** latest row per domain (`ROW_NUMBER() OVER (PARTITION BY domain ORDER BY file_name DESC)`)

| Column | Type | Description |
|---|---|---|
| `domain` | string | Lowercased domain (join key) |
| `page_url` | string | Full URL of the sampled page |
| `requests` | int | Number of HTTP requests on the page |
| `grabbed_text` | string | Scraped body text (truncated to 50 chars in DynamoDB) |
| `file_name` | string | Source filename (used for dedup ordering) |
| `has_exclusion_word` | boolean | Flagged if page contains exclusion keywords |
| `tier` | int | Content tier classification |
| `row_num` | int | Original row number from source |
| `rn` | int | Dedup rank (only `rn = 1` is kept) |

**Example rows:**

| domain | page_url | requests | has_exclusion_word | tier |
|---|---|---|---|---|
| moneyprodigy.com | https://www.moneyprodigy.com/easy-things-kids-can-make-and-sell-at-school | 8 | false | 2 |

---

## Pipeline Flow

```
bronze_lumen_attention  ─────────────┐
EMI - Raw.csv           ─────────────┤
bronze_page_speed       ─────────────┼──► JOIN on domain ──► SCORE & BUCKET ──► bronze_curationai
domain_categories       ─────────────┤                                               │
bronze_contextual_arc_all ───────────┤                                               ▼
df_performance (cpm)    ─────────────┘                                          DynamoDB
                                                                           (curationai_domain)
```

---

## Scoring Logic

Each metric is scored against a **benchmark value**. Scores range from 0–100.

| Metric | Benchmark | Direction | Notes |
|---|---|---|---|
| `attention` | 600 | Higher is better | Time-in-view (ms per 1000 impressions) |
| `speed` | 0.5 | Higher is better | Page performance score (0–1) |
| `impressions` | 1000 | Higher is better | Avg measured impressions |
| `ethical` | 40 | Higher is better | EMI ethical score |
| `cpm` | *(TBD)* | **Lower is better** | Cost per mille — scoring is inverted |

### Score formula (for higher-is-better metrics)

```
score = (value / benchmark) × 80           if value ≤ benchmark
score = 80 + min((value - benchmark) / benchmark, 0.25) × 80   if value > benchmark
score = min(score, 100)
```

### Bucket bands (for higher-is-better metrics)

| Bucket | Range |
|---|---|
| 1 | < 50% of benchmark |
| 2 | 50% – 80% of benchmark |
| 3 | 80% – 100% of benchmark |
| 4 | 100% – 150% of benchmark |
| 5 | ≥ 150% of benchmark |

> **`cpm` is inverted** — cheaper domains score higher. The bucket and score logic should be reversed so that lower CPM maps to bucket 5 / score ~100.

---

## Output Table: `hive_metastore.default.bronze_curationai`

### Schema

| Column | Type | Description |
|---|---|---|
| `domain` | string | Domain (primary key) |
| `impressions` | double | Avg measured impressions |
| `attention` | double | Attention score (ms/1000 imps) |
| `ethical` | double | EMI ethical score |
| `website_category` | string | IAB-style category |
| `speed` | double | Lighthouse performance score (0–1) |
| `cpm` | double | Cost per mille |
| `page_url` | string | Sampled page URL |
| `requests` | int | HTTP requests on sampled page |
| `grabbed_text` | string | Scraped page text |
| `file_name` | string | Source file for page-level row |
| `has_exclusion_word` | boolean | Exclusion keyword flag |
| `tier` | int | Content tier |
| `row_num` | int | Source row number |
| `rn` | int | Dedup rank (always 1) |
| `attention_bucket` | int | Attention bucket (1–5) |
| `score_attention` | double | Attention score (0–100) |
| `speed_bucket` | int | Speed bucket (1–5) |
| `score_speed` | double | Speed score (0–100) |
| `impressions_bucket` | int | Impressions bucket (1–5) |
| `score_impressions` | double | Impressions score (0–100) |
| `ethical_bucket` | int | Ethical bucket (1–5) |
| `score_ethical` | double | Ethical score (0–100) |
| `cpm_bucket` | int | CPM bucket (1–5, **inverted**) |
| `score_cpm` | double | CPM score (0–100, **inverted**) |
| `language` | string | Detected language from TLD |

### Example row

| Column | Value |
|---|---|
| `domain` | moneyprodigy.com |
| `impressions` | 69.0 |
| `attention` | 558.81 |
| `ethical` | null |
| `website_category` | Finance & Business |
| `speed` | 0.6227 |
| `cpm` | — |
| `page_url` | https://www.moneyprodigy.com/easy-things-kids-can-make-and-sell-at-school |
| `requests` | 8 |
| `has_exclusion_word` | false |
| `tier` | 2 |
| `attention_bucket` | 3 |
| `score_attention` | 74.51 |
| `speed_bucket` | 4 |
| `score_speed` | 99.64 |
| `impressions_bucket` | 1 |
| `score_impressions` | 5.52 |
| `ethical_bucket` | 5 |
| `score_ethical` | 100.0 |
| `language` | English |

---

## Language Detection

Assigned from domain TLD. Supported languages: English, Danish, French, German, Greek, Italian, Norwegian, Portuguese, Spanish, Swedish, Polish, Hungarian. Defaults to `"Unknown"`.

---

## Outputs

| Destination | Detail |
|---|---|
| Hive table | `hive_metastore.default.bronze_curationai` (overwrite mode) |
| DynamoDB table | `curationai_domain` (dropped and recreated on each run) |

> DynamoDB items are keyed by a generated UUID. `grabbed_text` is truncated to 50 characters before write.
