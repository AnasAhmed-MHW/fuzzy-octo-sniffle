---
title: Direct Buys
parent: SIGNAL
nav_order: 2
last_modified_date: 2025-02-14 12:00
---
# Direct Buy Data Processing

## Step 1: Creating a Direct Buy Data Template

The first step in the datastream pipeline involves creating a template for processing direct buy data. This template enables grouping by the **placement ID** and allows end-users to input values for **CPM, CPC, CPV, and CPVC**.

### Key Considerations:
- **Configurations:** Define filters and grouping columns.
- **Source Data:** Extracted from **Campaign Manager**.
- **Consistency:** Column names must remain uniform to ensure seamless processing.

## Step 2: File Upload & CPI Calculation

Once a file is uploaded to the **S3 bucket** `mh-directbuys`, the user must follow the table format established in Step 1. The system processes the provided cost-per values and computes the **CPI (Cost Per Impression)** for direct buys.

### Output:
A table containing **placement_adset_id** and **cost per impression** values.

## Integration within ETL

The `campaignmanager` module in the `datastream-etl` repository includes a **directbuys** module. This module:
1. Fetches the processed table for the client.
2. Joins the CPI data using **placement_id** and **date**.
3. Includes a **currency overwrite** feature to handle discrepancies between the user-provided currency and the API currency.

## Cost Hierarchy in `siteserved`

The `siteserved` module features a **calculate_local_spend** function, which determines the cost hierarchy based on different spend sources. The hierarchy follows this order:

1. **Siteserved Costs**
2. **Direct Buys**
3. **DV360 Costs** (from Campaign Manager API)
4. **General Spend** (from Campaign Manager API)


