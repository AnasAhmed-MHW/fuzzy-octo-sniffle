---
title: Raw table refresh
parent: Pinterest
nav_order: 2
last_modified_date: 2026-10-28 10:10
---

# Raw table refresh

**Task:** `Pinterest_New_Workflow` (depends on `Naming_Conventions`)  
**Notebook:** `/Repos/anas.ahmed@mediahubww.com/datastream-etl/etl/pinterest/Job/Pinterest Raw Table Refresh`  
**Cluster:** `0908-154440-758js3qc`

Same JDBC pattern as naming refresh, but loads **delivery / creative / campaign** partner tables (plus a subset of naming tables again).

---

## What happens

1. JDBC into `client_pinterest` on the same RDS cluster.
2. Loop tables → overwrite `raw.pinterest.{table}`.

## Tables refreshed

| Table | Role |
|---|---|
| `av_facebook_adset_db` | Meta delivery |
| `av_snapchat_creative_db` | Snapchat delivery |
| `av_reddit_adset_db` | Reddit delivery |
| `av_tiktok_creative_db` | TikTok delivery |
| `av_linkedin_creative_db` | LinkedIn delivery |
| `av_gads_campaign_db` | Google Ads (raw only in this job) |
| `av_teads_pbm_db` | Teads delivery |
| `av_thetradedesk_creative_db` | Trade Desk delivery |
| `av_facebook_naming_convention` | NC (also in naming task) |
| `av_gads_naming_convention` | NC |
| `av_snapchat_naming_convention` | NC |
| `av_tiktok_naming_convention` | NC |
| `av_reddit_naming_convention` | NC |

## Outputs

**`raw.pinterest.*`** Delta tables consumed by Social and Programmatic notebooks.

{: .tip }
> If a channel gold notebook fails on missing columns or empty NC joins, re-check that this task completed and the relevant `av_*` table was overwritten today.
