---
title: The TradeDesk
parent: SIGNAL
nav_order: 4
last_modified_date: 2025-09-22 12:00
---

# The Trade Desk pipeline

The Trade Desk spend data gets pulled from a report called "Global | TTD | SpendPlacement" and into an Adverity datastream also called "Global | TTD | SpendPlacement." If you need to add a new column, delete a column or edit the report in some kind of way, you need to create a brand new report and await 24 hours before it appears in Adverity. Broadly, this is what the pipeline looks like:

```mermaid
flowchart TD
    A[The TradeDesk] --> B[Adverity]
    B --> C[S3 Bucket]
    C --> D[Databricks - Siteserved Table]

```

## How to create a new report to pull from Trade Desk to Adverity

Use the account "ttd_api_multipartner_adverity@mediahubww.com" to create a report in The TradeDesk. When you create a report always use one of the pre-created templates, otherwise it won't appear in The TradeDesk: 

![screenshot 1](https://lh3.googleusercontent.com/pw/AP1GczO2VL_M5QNJ-qGPjyjWYndsfwHF_-3kLV8oi9HPUNahMRRHPO--GTcmhhbH-9txOQ4bXrXxUmP8oOpy98dF-7vVETLuGbhjzAUmOYLICsEEGNobYof7XGQ6Kv8DrvhILca6yZdzKUXWJA3fWH_o5rm5=w1505-h721-s-no-gm?authuser=0)

## Things to note are:

- You often have to wait a full 24 hours before the report appears in Adverity,
- Make sure you use the same ttd_api_multipartner_adverity@mediahubww.com authentication in Adverity,
- Take note of where you create the report in TradeDesk (is it in the New Balance advertiser account, the Celebrity Cruises advertiser account, the Mediahub Partner Seat?) as this could influence where you see the report in Adverity when you use the advertiser/partner dropdowns:

![screenshot 1](https://lh3.googleusercontent.com/pw/AP1GczN2yWd7MSpAAkoxhrZAR87pzZPKCuRruh2orri6yOczea1Ffz7dteAaXPXn6h4ARrcNZRl_Blp58REMYMhkdUCHIOR44OtRxOMVOCGY-B8jcsCHsqzludWtCTqAGFHiRGzt2Q6SUtO4fJx0C5N2qW0P=w1644-h847-s-no-gm?authuser=0)



