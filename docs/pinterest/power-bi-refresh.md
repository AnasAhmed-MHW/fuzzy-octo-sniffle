---
title: Power BI refresh
parent: Pinterest
nav_order: 6
last_modified_date: 2026-10-28 10:10
---

# Power BI refresh

**Task:** `PowerBI_refresh`  
**Depends on:** `Allchannel`  
**Type:** Databricks **Power BI task** (not a notebook)

Final step of [Pinterest Data Refresh](https://dbc-341b6afb-df67.cloud.databricks.com/jobs/657198646939030?o=7058903129942627): after all-channel gold is rebuilt, trigger a semantic model refresh so dashboards show the new day.

---

## Configuration (from job)

| Setting | Value |
|---|---|
| Connection | `powerbi-clientsecret-auth` |
| Auth | OAuth |
| Power BI workspace | **Pinterest x Mediahub** |
| Model | `signal$1 Overview$Performance Summary` |
| Storage mode | DirectQuery |
| Overwrite existing | false |
| Refresh after update | **true** |
| SQL warehouse | `a463da14fd376325` (Starter Warehouse) |

---

## Upstream dependency

Only runs if `Allchannel` succeeds — i.e. `uc_dev.pinterest.gold_allchannel_summary` (and namingconvention union) have been rebuilt from the day’s Social + Programmatic golds.

{: .tip }
> If Power BI looks stale but the job is green through Allchannel, check this task’s run logs and the Power BI workspace refresh history for OAuth / capacity errors.
