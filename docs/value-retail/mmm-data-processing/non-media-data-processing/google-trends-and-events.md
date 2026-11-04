---
title: Google Trends & marketing events
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 3
last_modified_date: 2026-10-28 09:50
---

# Google Trends & marketing events

S3 inputs under `s3a://mh-rawdata-valueretail/mmm/`.

---

## Google Trends

| | |
|---|---|
| **File** | `google_trends/Weekly Google Trends h1.csv` |
| **Grain** | Modelling week (already weekly) |
| **Transform** | Suffix all columns with `_gt` |
| **Join key** | `Modelling Week_gt` = FF week |

**Adds to final dataset:** Brand / category search-interest covariates.

---

## Marketing Events

| | |
|---|---|
| **File** | `marketing_events/Marketing_events_2026.csv` |
| **Grain** | Event date |
| **Transform** | Prefix columns with `ME_` |
| **Join key** | `ME_Date` |

**Adds to final dataset:** Event / promo flags on the matching modelling week.
