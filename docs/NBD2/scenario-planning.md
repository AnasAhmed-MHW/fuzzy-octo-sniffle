---
title: Scenario Planning
parent: NBD2
nav_order: 3
has_children: true
last_modified_date: 2026-02-24 12:00
---

![Last Revised](https://img.shields.io/badge/last%20revised-2026--02--19-blue?style=flat-square)

# NBD for Scenario Planning

The Scenario Planning module helps you decide what to do next by generating, forecasting, and optimizing media plans using your MMM models and reinforcement learning.

## Overview

NBD offers three main scenario planning capabilities:

1. **[Generate New Plans](../generate-plan)** - Create optimal media plans from scratch
2. **[Forecast Plans](../forecast-plan)** - Predict KPI outcomes for existing plans
3. **[Optimize Plans](../optimise-plan)** - Refine existing plans to maximize impact

All three use your econometric models to predict future performance and apply reinforcement learning to find optimal allocations.

## Understanding the Risk Slider

The risk slider (change threshold) controls constraint boundaries:

<!-- SCREENSHOT: Risk slider control showing scale from 1-5 with explanatory labels -->

| Risk Level | Meaning | When to Use |
|------------|---------|-------------|
| **1-2** | Very conservative | You want minimal changes vs. historical spend |
| **3** | Balanced (default) | Normal optimization with reasonable flexibility |
| **4-5** | Aggressive | Major strategy change or you want maximum flexibility |

The risk level expands or narrows the min/max spend boundaries for each channel based on historical data.
Higher risk = wider boundaries = more room to reallocate.

## Working with Constraints

### When to Use Default Constraints

In most cases, **keep the default constraints** and adjust only the risk slider. This is sufficient for standard optimization.

### When to Edit Constraints Manually

Edit constraints when:

1. **Yellow Highlights** - NBD couldn't estimate spend for a channel (highlighted in UI)
2. **Major Strategy Shift** - You're planning 2x or more spend vs. last year
3. **Fixed Investments** - Some spend is already booked and cannot be changed (set min=max=booked amount)
4. **Channel Exclusions** - You want zero spend in a channel (set min=0, max=0)

<!-- SCREENSHOT: Constraints editor showing channel min/max values with one channel highlighted in yellow -->

### Constraint Types

- **Channel Boundary** - Min/max total spend for each channel
- **Weekly Boundary** - Max spend per week (prevents unrealistic week-over-week spikes). You may notice this in a generated plan where a channel shows the same spend amount for several consecutive weeks — this means it has hit its weekly cap.
- **Regional Boundary** - Min/max spend per market
- **Temporal Constraint** (optimize only) - Keeps spend within ±2 weeks of original timing


## Benchmark Types

Benchmarks provide context for your optimized plan by comparing it to alternatives.

| Benchmark Type | What It Is | When to Use |
|----------------|------------|-------------|
| **Default** | Based on average weekly spend × number of weeks | Compare optimized plan vs. "business as usual" |
| **Historical** | Actual spend from the same period last year | Compare vs. what you did before (useful for YoY analysis) |
| **Channel Spend Mix** | Historical channel mix scaled to your new budget | Compare optimized allocation vs. historical allocation |

**Note:** The Historical benchmark often shows large KPI differences because the historical plan wasn't optimized.

For conceptual details, see [Glossary: Benchmarks](../glossary#benchmarks).

## Sharing Plans with Others

### Generating a Share Code

After creating a scenario, NBD provides a **Share Code**. Copy this code and send it to other NBD users via email or chat.

### Loading a Shared Plan

1. Go to **Scenario Planning > Plan Generator**
2. Enter the Share Code in the **Import Plan** field on the right
3. Click **Load This Plan** to view the scenario

Shared plans are view-only but can be used as a starting point for your own scenarios.

## Common Workflows

### Workflow 1: Annual Planning
**Goal:** Create next year's media plan

1. Use **[Generate New Plan](../generate-plan)**
2. Set full year date range
3. Set total annual budget
4. Use Risk Level 3-4 (some flexibility)
5. Select "Historical" benchmark to compare vs. last year
6. Review and refine constraints if needed
7. Share results with stakeholders using Share Code

### Workflow 2: In-Flight Optimization
**Goal:** Improve a plan that's already running

1. Use **[Optimize Existing Plan](../optimise-plan)**
2. Import current spend for remaining weeks
3. Lock any spend that's already booked (set min=max)
4. Adjust constraints for flexible channels
5. Optimize and implement recommended changes

### Workflow 3: Budget Scenario Comparison
**Goal:** Show what's possible at different budget levels

1. Use **[Generate New Plan](../generate-plan)** with Budget A
2. Note the Share Code
3. Run again with Budget B
4. Run again with Budget C
5. Use **[Forecast](../forecast-plan)** to predict all three scenarios
6. Compare KPI outcomes and share all three Share Codes with stakeholders


## Best Practices

1. **Start with Default Settings** - Use Risk Level 3 and default constraints first
2. **Validate Results** - Check if recommended spend makes business sense
3. **Iterate** - Run multiple scenarios with different parameters
4. **Lock Known Commitments** - Set constraints for any pre-booked spend
5. **Consider Seasonality** - NBD accounts for seasonal patterns in the models
6. **Share Early** - Use Share Codes to collaborate with stakeholders before finalizing
7. **Document Decisions** - Save Share Codes and notes about why you chose specific scenarios

## Troubleshooting

### "Channel highlighted in yellow"
**Issue:** NBD couldn't estimate historical spend for this channel

**Solution:** Manually set min/max constraints for that channel

### "Optimization failed"
**Possible causes:**
- Constraints are too restrictive (total min > budget or total max < budget)
- Date range has no historical data
- Model files are missing or corrupted

**Solution:** Check constraints, verify date range, contact support if issues persist

### "Results seem unrealistic"
**Possible causes:**
- Risk level too high
- Constraints too loose
- Model may not capture recent market changes

**Solution:** Lower risk level, tighten constraints, or lock specific channels to expected ranges
