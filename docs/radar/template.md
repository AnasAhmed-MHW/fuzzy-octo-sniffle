---
title: MediaPlan Template
parent: RADAR
nav_order: 3
last_modified_date: 2024-06-20 12:00
---

# The Template

## Overview

The MediaPlan Tempalate has been a long process to develop and much a pain. 

## What to look out for when creating one

1. Use the current Mediahub Template as a base template.
2. Understand what changes you need to make to the manadatory and optional columns.
   1. This should be informed by the need for planned v actual breakdowns you need to do and the visuals you need to create
3. Ensuring the dropdowns in the table match the taxonomy breakdowns
4. Top left section (meta data) should be values that are consistent across the whole tab

## What to look out for when creating a new Version

When making changes to the excel template you need to look out for:

1. Making sure the dimension (category) column headers are consistent across the tabs
2. Making sure a single "line item" is composed of the same number of rows.
3. The weekly breakdowns are consistent across all the tabs (and are relavent for the year)


## Common Issues

- Numbers are not registering as numbers, wither due to an input error, or due to certain excel settings - metrics are sometimes not registered as numebrs. 
- Changes to the template - there are times when there is an extra row added to the "line item" therefore the number of rows merged is different
- Weekly breakdowns dont sum to the net net costs. 
- Merged dimension values are not filling down correctly.

When looking at issues try to run the Notebook by itself to isolate which step is causing the issues. 
Have a look at the "processed" excel in the processed folder to see if the ExcelProcessor has manipulated the excel incorrectly., 

