---
title: Optimise a Plan
parent: Scenario Planning
grand_parent: NBD2
nav_order: 3
last_modified_date: 2026-02-24 12:00
---

![Last Revised](https://img.shields.io/badge/last%20revised-2026--02--19-blue?style=flat-square)

# Optimise an Existing Plan

Use the Plan Optimiser when you have a plan that's already in progress or partially actioned, and you want to improve it.

## Step-by-Step

1. **Select Date Range** - The period to optimise

2. **Choose Channels** - Select which channels are in your existing plan

3. **Import Your Plan** - Copy and paste from Excel/spreadsheet row by row

<!-- SCREENSHOT: Existing plan import interface showing paste area and channel mapping -->

4. **Adjust Total Budget** (optional) - Increase or decrease if needed

5. **Set Constraints** - Define how much flexibility NBD has:
   - Leave empty for automatic constraints based on risk slider
   - Set min=0, max=0 to **lock** a channel (prevent any changes)
   - Manually set boundaries if you have specific requirements

<!-- SCREENSHOT: Constraints editor with some channels locked and others with flexible boundaries -->

6. **Optimise** - NBD reallocates budget to maximize KPI while respecting constraints

## Output

- **Optimised Media Plan** - Recommended weekly spend by channel and market
- **Comparison View** - Side-by-side comparison of original vs. optimised plan
- **Forecasted KPI Improvement** - Expected performance gain
- **Share Code** - Code to share this scenario with other users

<!-- SCREENSHOT: Optimised vs original comparison showing spend changes and KPI improvement -->

## Key Difference from Generate

- **[Generate](../generate-plan)** starts from scratch using historical spend as a guide
- **Optimise** starts from your actual plan and makes targeted improvements

The optimiser also uses **temporal constraints** (±2 weeks) to keep the optimised plan similar to your input, preserving domain knowledge like campaign timing or product launches.

## Temporal Constraints

When optimizing an existing plan, NBD applies temporal constraints to maintain the timing structure of your original plan. This means:

- Spend for each channel stays within ±2 weeks of when you originally scheduled it
- Campaign timing and strategic decisions are preserved
- Product launches and seasonal events aren't disrupted by optimization

This ensures the optimiser improves your plan without ignoring the business context you built into the original timing.

For technical details, see [Glossary: Constraints](../glossary#constraints).
