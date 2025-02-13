---
title: Adjusting Taxonomy
parent: Analyst Engineering Guide
nav_order: 3
last_modified_date: 2025-01-23 12:00
---

# Taxonomy Tweaks

The Taxonomy is a painful area for account teams and biddable teams. Often taxonbomy errors are not resolved fast enough, leading to persistant errors. 

There is a ‘statute of limitations’ so to speak on very old campaigns where even if a name is corrected in the platform, the platforms API no longer updates this value, for these cases we have an overrides sheet, where we can continue to override incorrect names irrespective of how old the error is. 

---


## Platform Limitations

Each platform imposes its own restrictions on how long campaign names can be updated:  

| **Platform**      | **Update Window**                |  
|--------------------|----------------------------------|  
| **Amazon Ads**     | Max 60 days                     |  
| **Pinterest**      | Max 180 days                    |  
| **Reddit**         | Max 90 days                     |  
| **SA360**          | Max 365 days                    |  
| **TikTok**         | Max 365 days                    |  
 

{: .warning}
There are platforms that do not change a name when there is no spend assigned. <br> _Example includes: Meta, Tiktok, Google Ads_

---

## Substitution Process  

To address these limitations, we’ve implemented a **Substitution Process** that integrates into the pipeline. This process ensures incorrect names can still be overridden where API restrictions or other limitations prevent updates.  

{: .note}
We keep these seperate from the governance docs as to should you wish to allow access to teams outside of D&A. 

<br>

<table>
    <tr>
        <td><a href="https://docs.google.com/spreadsheets/d/1m4TUDxEhlw5fqAKqxxS4PttI-6EUanjHtF3kXfnGjU0/">Value Retail</a></td>
        <td><a href="https://docs.google.com/spreadsheets/d/1CbnbiYIrV2spAJZAH91PEb8HGkRzOJFyJ-WhxeB4i9I">New Balance</a></td>
        <td><a href="https://docs.google.com/spreadsheets/d/1ghYo4Pm_dNQv6Vv4eU6aqS8DFtD3_q3y1Z-xAn8M-5k">AkzoNobel</a></td>
    </tr>
</table>

<br>

{: .warning}
Please ensure there is no duplications. This process will take the first instance of the name. There also may be unintended duplications with duplications here. 

---

## Acronyms in Taxonomy  

Many clients prefer using acronyms due to character limits on some platforms. However, this can make dashboards less readable.  

To standardise and improve readability, the **FieldCodes** tab in the governance sheet allows for the substitution of acronyms with their full, readable names.  

### Steps for Acronym Substitution:  
1. Locate the `FieldCodes` tab in the governance document.  
2. Fill in the following details:  
   - **Category:** Align this with the header in the `Shared Values` tab.  
   - **Acronym:** The short form or incorrect name to be replaced.  
   - **Word:** The full, readable name to be used in dashboards.  

{: .tip}
This process also supports correcting undetected misspellings <br> _Example includes: "Ingoldstadt" → "Ingolstadt"_.  
