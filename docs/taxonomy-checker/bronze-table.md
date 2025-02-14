---
title: Inital Workflow
parent: Taxonomy Checker
nav_order: 4
last_modified_date: 2025-02-03 12:00
---

# Inital Workflow - Generating the input tables


The input table is created just before it is pushed into the taxonomy checker. 
This is generated through a few different steps. 


1. Files from S3 Bucket
   Based on the client config the script will look for "channel" folders in the canonical folder and store the filenames with the latest date for each channel

2. Bronze Channel Tables
   These files will then be ingested to a `raw.bronze_{channel}_namingconv` table.

3. Fetching SIGNAL Data
   A spark dataframe with the corresponding SIGNAL data for the channel will be fetched. 

4. For each of the files in the S3 bucket a few things will happen:
   1. fetch the file
   2. unify the column structures. ie adset, placements, adgroup all get unified to placement_adset. (look for the function `clean_granularity`)
   3. the bronze schema is enforced

5. SIGNAL Join
   We join the SIGNAL data onto the the naming convention bronze table. This is to get the max activity date, the spend and impressions for that taxonomy line. 
   Being below the thresholds or being before the taxonomy date will result in the taxonomy value state being inactive.

6. Manual Tables
   Should you have done a pre-process step this is unioned onto the table. The API data is joined based on the 'source' column

7. Define Channel
   Based on the channel name, data source and other columns the taxonomy values are categorised into 'channels' these need to correspond to the channels in the governance doc. 

{: .note}
The state of the taxonomy value is based on impressions and spend. If there is _any_ spend and a certain number (deinfed in config) of impressions these will be active

**Problems**
We've gone through a few back and forth with these. Generally when people say the ad should be inactive or incorrect - verify the claim! Generally we've seen the data is correct. 

Understand how things are joining between the SIGNAL and Naming Convention Tables


8. Substitution
   This is what happens next. If available it will take the vslues from the google sheet and substitute the name values with the new name values in the google sheet based on the IDs in the google sheet. 

{: .warning}
We've seen people duplicate values in the google sheet. We've seen people forget and make mistakes and blame the API. Check these values are correct - or when flagged check these sheets!


