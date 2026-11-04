---
title: All channel
parent: Pinterest
nav_order: 5
last_modified_date: 2026-10-28 10:10
---

# All channel

**Task:** `Allchannel`  
**Depends on:** Facebook, Snapchat, LinkedIn, Reddit, Programmatic, Tiktok (all must succeed)  
**Notebook:** `/Repos/anas.ahmed@mediahubww.com/datastream-etl/etl/pinterest/Job/All Channel`  
**Cluster:** `0908-154440-758js3qc`

Downstream **union** of every partner gold creative table into one reporting fact, plus a harmonised namingconvention union.

---

## Creative summary

```sql
CREATE OR REPLACE TABLE uc_dev.pinterest.gold_allchannel_summary AS
-- UNION ALL of:
--   gold_facebook_creative
--   gold_linkedin_creative
--   gold_reddit_creative
--   gold_snapchat_creative
--   gold_tiktok_creative
--   gold_teads_creative
--   gold_thetradedesk_creative
-- WHERE date >= '2025-01-01'
```

**Output:** `uc_dev.pinterest.gold_allchannel_summary`

---

## Validation cell

Side-by-side **pre-union vs post-union** metrics per source (row count, spend, impressions, clicks) with `PASS` / `FAIL` when totals disagree beyond a small spend tolerance.

Partner → source mapping in gold includes Meta family → `facebook`, and Trade Desk sub-partners (`Digital Turbine`, `Ogury`, `Seedtag`, etc.) → `thetradedesk`.

---

## Naming convention union

**Output:** `uc_dev.pinterest.gold_allchannel_namingconvention`

`UNION ALL` of per-partner namingconvention golds with column alignment:

| Source | Ad group field mapped from |
|---|---|
| Facebook | native columns |
| LinkedIn | `creative` → ad_group, `creative_name` → creative |
| Snapchat / TikTok / Reddit | `ad_name` → ad_group (`naming_string` may be NULL until those notebooks re-expose it) |
| Teads | `placement_name` → ad_group |
| Trade Desk | `placement_name` → ad_group; naming_checker / naming_string often NULL |

---

## Downstream

On success, the job runs [Power BI refresh](power-bi-refresh), which reads the all-channel (and related) model in the **Pinterest x Mediahub** workspace.
