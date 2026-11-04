---
title: Email
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 2
last_modified_date: 2026-10-28 09:50
---

# Email

| | |
|---|---|
| **File** | `s3a://mh-rawdata-valueretail/mmm/Email Data/email_sends_2026 + 25 .csv` |
| **Grain** | Week commencing × village code × campaign group |
| **Metrics** | Sum Emails_sent, sum Emails_Opened |
| **Variable pattern** | `{VillageCode}_{group}` e.g. `BV_Membership` |

**Processing:** Map village codes to names for QA; bucket campaigns via `map_campaign_to_group` (Membership, Retargeting, Newsletter, Discount, Amber Room, Reward, Other); pivot sends and opens. High variable count, but still left-joined into the master frame on `Week_Commencing`.

**Adds to final dataset:** CRM email activity split by campaign theme.
