---
title: Problem Channels
parent: Adverity
nav_order: 99
last_modified_date: 2024-01-20 13:00
---

# Problem Channels Requiring Context  

Certain platforms or channels have unique challenges when fetching data via APIs. Below are the issues and corresponding solutions to address these limitations.

## Google Ads + Search Ads 

- **Issue**:  
  - Campaign types vary in availability based on the level of granularity.  
    - **Keyword Level**: Only Search Campaigns can be fetched.  
    - **Ad Level**: Fetches Display, YouTube, and Search Campaigns.  
    - **Campaign Level**: Includes Performance Max, Shopping (Display, YouTube, and Search).  
  - **Note**: Campaign-level data is the most comprehensive, while granular levels may have gaps.  

- **Solution**:  
  - Create separate datastreams for each level of granularity.  
  - Union these datasets within **Databricks** to provide a complete view.  


## Pinterest 

- **Issue**:  
  - Shopping Campaigns are not fetched at the **Ad Level**.  

- **Solution**:  
  - Create multiple datastreams to cover missing levels.  
  - Combine these datastreams in **Databricks** to consolidate data.  


## Reddit

- **Issue**:  
  - The API does not fetch **High Impact Campaign Types** at any granularity.  

- **Solution**:  
  - Coordinate with the **Biddables/Account Team** to obtain a manual export of the data.  
  - Integrate manually fetched data into the pipeline.  


## Amazon 

- **Issue**:  
  - The API supports fetching data for only one **Advertising Channel** at a time.  

- **Solution**:  
  - Duplicate the datastream and configure the dropdown to select different Advertising Channels for each datastream.  


## The Trade Desk (TTD)

- **Issue 1**:  
  - API reports must be created manually through an account, linked to another API account.  

- **Solution**:  
  - Generate reports manually using **ttd_api_multipartner_adverity@mediahubww.com**.  
  - Link these reports to the API Adverity account: **ttd_api_multipartner1@mediahubww.com**.  

- **Issue 2**:  
  - New or regional TTD partners require approval and process alignment with multiple TTD representatives.  
  - Different partners cannot be included in the same report.  

- **Solution**:  
  - For each partner, create separate datastreams.  
  - Liaise with TTD representatives to ensure smooth onboarding and integration.
 
- **Issue 3**:  
  - Figures look incorrect when you export a CSV file from Adverity.

- **Solution**:  
  - Make sure when you export a CSV file and are prompted to convert the figures, select yes.
