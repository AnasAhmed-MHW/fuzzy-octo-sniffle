---
title: PR
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 5
last_modified_date: 2026-10-28 09:50
---

# PR — Social, Print, Online

Files under `s3a://mh-rawdata-valueretail/mmm/PR/`.

| Channel | File | Core metrics |
|---|---|---|
| Social | `social_fy_cleaned+2026.csv` | MIV USD, Followers, engagement rate, Likes, Shares, Views |
| Print | `print_fy_cleaned + 2026.csv` | MIV USD, Potential Reach |
| Online | `online_fy_cleaned + 2026.csv` | MIV USD, Potential Reach |

**Processing (all three):** Map village → code; classify Domestic / International / Ignore from location vs village home country (`map_country_village`); convert MIV GBP × **1.2529** → USD; Monday week; pivot.

**Variable pattern:** `PR_{Code}_{Social|Print|Online}_{Domestic|International|Ignore}`

**Adds to final dataset:** Earned-media value and reach, split domestic vs international.

{: .note }
> PR MIV FX is hard-coded at **1.2529** (GBP → USD). Recalibrate if FX assumptions change for a new modelling window.
