---
title: Programmatic
parent: Pinterest
nav_order: 4
last_modified_date: 2026-10-28 10:10
---

# Programmatic

**Task:** `Programmatic` (depends on `Pinterest_New_Workflow`; parallel with Social)  
**Notebook:** `/Repos/anas.ahmed@mediahubww.com/datastream-etl/etl/pinterest/Job/Programmatic/Programmatic`  
**Cluster:** `0908-154440-758js3qc`

Builds gold creative + namingconvention tables for **The Trade Desk** and **Teads**. Same job stage as social, different channel / cost rules.

---

## The Trade Desk

| | |
|---|---|
| **Input** | `raw.pinterest.av_thetradedesk_creative_db` (no separate NC table in this notebook) |
| **Outputs** | `uc_dev.pinterest.gold_thetradedesk_namingconvention`, `gold_thetradedesk_creative` |

**Processing highlights**

- Filter / aggregate for advertiser **Pinterest**
- Parse taxonomy from `creative_name` directly; **platform / partner** often from naming **chunk 6**
- Creative gold: channel = `media_type`; **`media_cost = costs / 0.85`** (fee gross-up)
- Hard filter **`year(date) = 2026`** on NC/creative paths in the current notebook; currency **GBP**
- Video quartile fields often **NULL** on TTD gold
- Impressions &gt; 0 filter on creative gold

{: .note }
> Comments in-notebook mention historic ADTAG joins that are not implemented in the current export.

---

## Teads

| | |
|---|---|
| **Inputs** | `raw.pinterest.av_teads_pbm_db`, `av_teads_naming_convention` |
| **Outputs** | `uc_dev.pinterest.gold_teads_namingconvention`, `gold_teads_creative` |

**Processing highlights**

- Closer to the **social bronze → NC → creative** pattern
- Channel from line item: **Programmatic OLV** vs **Programmatic Display**
- Same 17- vs 19-chunk naming rules as social (`%PIN1%`, week positions by year)
- Partner fixed as **Teads**; currency GBP; video_views aligned to video_starts in places

---

## Validation

Notebook compares raw vs bronze spend for Trade Desk + Teads and can **Python hard-fail** (same style as Facebook) if variance is too high.

## Vs social

| Aspect | Social | Programmatic |
|---|---|---|
| Channel | Always `Paid Social` | TTD: `media_type`; Teads: OLV vs Display |
| Partner | Fixed platform name | TTD: from naming chunk; Teads: fixed |
| NC table | Always present | TTD: parse creative_name only |
| Cost | Pass-through | TTD: `/ 0.85` |
| Geo | UK + US (Reddit UK-only) | UK / GBP oriented in current logic |
