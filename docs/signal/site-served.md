---
title: Site Served
parent: SIGNAL
nav_order: 3
last_modified_date: 2025-02-14 12:00
---

# Site Served Data

The purpose of the siteserved pipeline is to ensure DSP data can be ingested into Campaign Manager through the `prod.global.gold_siteserved_placement` table

This is done through reading the files in the S3 bucket `mh-rawdata-global` 
The notebook looks for the S3 Bucket path `global/display/dsp_spend` 
And then loops through the `AVAILABLE_CHANNELS` in the constant file (expecting folders with the same name). 

{: .important}
There is a date range in the Site served notebook so if you are doing historicals then you will need to apply a changed date range


Have a read through of the README file in th esiteserved folder to understand how to add a new channel. 

