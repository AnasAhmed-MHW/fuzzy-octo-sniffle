---
title: Naming convention refresh
parent: Pinterest
nav_order: 1
last_modified_date: 2026-10-28 10:10
---

# Naming convention refresh

**Task:** `Naming_Conventions` (first in the job — no dependencies)  
**Notebook:** `/Repos/anas.ahmed@mediahubww.com/datastream-etl/etl/pinterest/Job/Pinterest Naming Convention Raw Refresh`

Pulls **naming-convention** tables from MySQL RDS into Unity Catalog raw Delta so later channel notebooks can join delivery to taxonomy strings.

---

## What happens

1. Open JDBC to RDS host `mlmdata-analytics-cluster…eu-west-1.rds.amazonaws.com`, database **`client_pinterest`** (MariaDB driver).
2. Connectivity check (`nc` to port 3306).
3. For each table in the list below: `spark.read.jdbc` → `overwrite` to `raw.pinterest.{table}` (`mergeSchema`).

## Tables refreshed

| MySQL / Delta table |
|---|
| `av_facebook_naming_convention` |
| `av_gads_naming_convention` |
| `av_linkedin_naming_convention` |
| `av_reddit_naming_convention` |
| `av_snapchat_naming_convention` |
| `av_teads_naming_convention` |
| `av_tiktok_naming_convention` |
| `av_thetradedesk_naming_convention` |

## Outputs

All written as **`raw.pinterest.av_*_naming_convention`**.

{: .note }
> Google Ads (`av_gads_*`) is refreshed into raw here, but the current job DAG does **not** include a Search notebook task — only Social + Programmatic + All Channel + Power BI.
