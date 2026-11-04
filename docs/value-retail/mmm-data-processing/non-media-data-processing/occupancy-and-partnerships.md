---
title: Occupancy & partnerships
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 4
last_modified_date: 2026-10-28 09:50
---

# Occupancy & partnerships

S3 inputs under `s3a://mh-rawdata-valueretail/mmm/`.

---

## Occupancy

| | |
|---|---|
| **File** | `Occupancy/Occupancy 25+26Q1 Upd (2).csv` |
| **Grain** | Week commencing × village |
| **Metric** | Avg of daily Open-Unit Size |
| **Variable pattern** | `{Village Name}_Occupancy` |

**Adds to final dataset:** Retail unit occupancy as a supply-side / capacity control by village.

---

## Partnerships (sales & redemptions)

| | |
|---|---|
| **Active files** | `partnerships/Partnerships_sales_FY.csv`, `Partnerships_Redemptions_FY.csv` |
| **Historic (ignore)** | `Partnerships.csv`, `Partnerships_redemptions.csv` — marked historic in the notebook |
| **Grain** | Week start × village code × partner segment |
| **Variable pattern** | `Partner_{Code}_Sales_{Segment}` / `Partner_{Code}_Redemptions_{Segment}` |

**Processing:** Melt week columns → long; map segments via `Partner_segment_to_variable`; conditional week-date (+7 days except week 53 24); pivot; **merge redemptions ⟕ sales** into `joined_partnerships`.

**Adds to final dataset:** Partner-driven sales and redemptions by segment (Corporate, Institutional, Mobility, Financial, Accommodation, Marketing, Travel, Buyers, Expats, GAP, etc.).
