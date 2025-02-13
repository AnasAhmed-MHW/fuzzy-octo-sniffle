---
title: Gold Tables
parent: RADAR
nav_order: 5
last_modified_date: 2024-06-20 12:00
---


# Gold Tables

Creating the gold media plan tables depends on how the SIGNAL Tables are formatted. Ensure you are filtering to the latest mediaplan

Few Methods

**Ideal**

1. Aggregate the SIGNAL tables to the Mandatory columns within the mediaplan.
2. Use the parsed table to ensure the column headers are the same as the mediaplan table
3. Join MediaPlan table with the Aggregated SIGNAL table
4. Actual costs should come from the SIGNAL table and planned activity from the MediaPlan

**Second Method**

When the join cannot happen between SIGNAL and MediaPlan tables. Then filter out SIGNAL channels from the MediaPlans and then Union the SIGNAL data

Issues with this.
1. Planned v actuals are difficult
2. Filtering out channels/ publishers may cause issues as you might need to take some from the mediaplan and some from SIGNAL tables

**Planned v Actuals MediaPlan**

Currently the _latest_ submitted mediaplan is the one that is used / the state is "active". 
This however, the script results in the daily / weekly breakdowns of the planned and actual costs exactly the same.

A method to get around this. 

1. Create a table with the latest version of the mediaplan with _all_ planned values and no _actual_ values. 
2. This will be your complete **planned** version. 
3. Join onto a gold table based on the mandatory columns and dates (as you cannot be certain if the line items will stay in the same section)


