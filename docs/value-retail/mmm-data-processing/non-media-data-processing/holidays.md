---
title: Holidays
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 6
last_modified_date: 2026-10-28 09:50
---

# Holidays

| | |
|---|---|
| **File** | `s3a://mh-rawdata-valueretail/mmm/holidays/Holidays_cleand (2).csv` |
| **Join key** | `Week_Commencing` |

**Adds to final dataset:** Public / school holiday indicators by week (and often by market/village columns already in the file).

{: .warning }
> Filename spelling (`Holidays_cleand`) is brittle — updating the source usually means changing the `FILE_HOL` constant in the Non-Media notebook.
