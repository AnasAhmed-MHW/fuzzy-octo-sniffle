---
title: Organic & owned digital
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 1
last_modified_date: 2026-10-28 09:50
---

# Organic & owned digital

S3 inputs under `s3a://mh-rawdata-valueretail/mmm/`. All pivoted to Monday week grain and left-joined in [Join & outputs](join-and-outputs).

---

## Organic Social

| | |
|---|---|
| **File** | `Organic_Data/Organic Social MMM 2025 + 2026  Data.csv` |
| **Grain after transform** | Week commencing × village |
| **Metrics pivoted** | Sum of Total Engagements, sum of Post Reach |
| **Variable pattern** | `{Mapped_Village}_Social` |

**Processing:** Parse `PublishedTime`, derive Monday week, fix Maasmechelen spelling, drop null weeks, pivot.

**Adds to final dataset:** Per-village organic social engagement and reach columns joined on `Week_Commencing`.

---

## Organic Search

| | |
|---|---|
| **File** | `Organic_Data/organic_Search 2025 + 2026 Q1.csv` |
| **Grain** | Week start × village |
| **Metric** | Sum of Sessions |
| **Variable pattern** | `{village}_Search` |

**Processing:** Clean village names / session number formatting; ISO week + year → date, then **+7 days** offset; pivot sessions.

**Adds to final dataset:** Organic search session volume by village per modelling week.

---

## Website

| | |
|---|---|
| **File** | `Website_Data/website_data 2025 + 2026 Q1.csv` |
| **Grain** | Week start × village |
| **Metric** | Sum of Sessions |
| **Variable pattern** | `{village}_Website` |

**Processing:** Same ISO-week → date +7 day pattern as Organic Search.

**Adds to final dataset:** Website session volume by village — demand / owned-digital control for MMM.
