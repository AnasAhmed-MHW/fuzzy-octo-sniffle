---
title: Generate a Plan
parent: Scenario Planning
grand_parent: NBD2
nav_order: 1
last_modified_date: 2026-02-24 12:00
---

![Last Revised](https://img.shields.io/badge/last%20revised-2026--02--19-blue?style=flat-square)

# Generate a New Plan

Use the Plan Generator when you're starting fresh and want NBD to recommend the best media allocation.

## Step-by-Step

1. **Set Date Range**
   - Select start and end dates for your media plan
   - NBD optimizes by week, so choose whole weeks when possible

<!-- SCREENSHOT: Date range picker showing start and end date selection -->

2. **Choose Risk Level** (slider: 1-5, default: 3)
   - Controls how much channel spend can differ from historical norms
   - **1** = Very conservative (minimal changes)
   - **3** = Balanced (recommended default)
   - **5** = Aggressive (maximum flexibility)
   - See [Understanding the Risk Slider](../scenario-planning#understanding-the-risk-slider) for details

<!-- SCREENSHOT: Risk slider control showing values 1-5 with default at 3 -->

3. **Name Your Plan**
   - Give it a memorable name for future reference
   - Example: "Q2 2026 UK Plan" or "Black Friday US Scenario"

4. **Select KPI**
   - Choose which business metric to maximize
   - Examples: transactions, visits, brand awareness
   - If unsure, use your primary business objective

5. **Choose Markets**
   - Select one or more markets to optimize
   - NBD can optimize across multiple markets simultaneously

<!-- SCREENSHOT: Market selection interface with multiple market checkboxes -->

6. **Set Total Budget**
   - Enter the total budget across all selected markets
   - NBD will allocate this optimally across channels and markets

<!-- SCREENSHOT: Budget input field with currency formatting -->

7. **Review/Edit Constraints** (optional)
   - Default constraints are based on historical spend + risk level
   - Click "Edit Constraints" to manually adjust minimum/maximum spend by channel or market
   - See [Working with Constraints](../scenario-planning#working-with-constraints) for guidance

<!-- SCREENSHOT: Constraints editor showing channel min/max values in a table format -->

8. **Select Benchmark Type**
   - Choose how to compare your optimized plan against historical norms
   - See [Benchmark Types](../scenario-planning#benchmark-types) for details

9. **Generate**
   - Click "Generate" to start the optimization
   - Results typically take 1-5 minutes depending on complexity

## Output

NBD returns:

- **Recommended Media Plan** - Weekly spend by channel and market
- **Forecasted KPI** - Expected performance
- **Benchmark Comparison** - How your plan compares to historical or default spending
- **Share Code** - Code to share this scenario with other users

<!-- SCREENSHOT: Results page showing media plan table, KPI forecast, and benchmark comparison -->
