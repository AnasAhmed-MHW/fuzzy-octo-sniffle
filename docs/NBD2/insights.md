---
title: Insights
parent: NBD2
nav_order: 2
last_modified_date: 2026-02-24 12:00
---

![Last Revised](https://img.shields.io/badge/last%20revised-2026--02--19-blue?style=flat-square)

# NBD for Insights

The Insights module provides a comprehensive view of media performance, helping you understand what happened with your media investments.

## Overview

Insights are organized into two main categories:

1. **Geographic Insights** - Compare and contrast media performance across markets
2. **Media Touchpoint Insights** - Understand individual channel performance

All insights are derived from your econometric models (MMM outputs) and show media contribution, cost efficiency, and comparative performance.

## Geographic Insights

Geographic insights help you understand similarities and differences in media effectiveness across markets.

### Global Meta-Analysis

The Global Meta-Analysis provides a comprehensive view of:

- **Media Investment by Market** - Total spend across all markets
- **Media Contribution** - How much each market's media contributed to the KPI
- **Cost Efficiency** - Cost per KPI unit (e.g., cost per visit, cost per transaction)
- **Channel Contribution** - Total contribution of each media channel across all markets

<!-- SCREENSHOT: Global meta-analysis view showing market comparison table with spend, contribution, and efficiency metrics -->

**Use this view to:**
- Identify markets with the highest ROI
- Compare cost efficiency across regions
- Understand which channels perform well globally

### Market Analysis

Market Analysis drills down into individual markets, showing:

- **Media Investment by Channel** - Spend breakdown within a specific market
- **Channel Contribution** - How each channel performed in that market
- **Channel Efficiency** - Cost per KPI unit for each channel

<!-- SCREENSHOT: Market analysis drilldown showing single market with channel-level breakdown -->

**Use this view to:**
- Understand market-specific dynamics
- Identify outlier channels (unusually high or low performance)
- Tailor strategies to local market conditions

## Media Touchpoint Insights

Media Touchpoint Insights focus on individual channels and how they perform across markets.

### Touchpoint Analysis

This view provides:

- **Response Curves** - How channel effectiveness changes with spend
- **Cross-Market Comparison** - How the same channel performs in different markets
- **Contribution Metrics** - Total impact of each touchpoint
- **Efficiency Metrics** - ROI and cost-per-KPI by touchpoint

<!-- SCREENSHOT: Touchpoint analysis view showing channel comparison across markets with contribution and efficiency charts -->

**Use this view to:**
- Identify similarities and outliers across markets
- Understand which regions a channel performs best in
- Optimize channel-specific strategies
- Set realistic expectations for channel performance

### Understanding Response Curves

Response curves show how incremental spend affects incremental return. They help you understand whether a channel is under-invested (more spend would drive significant returns) or saturated (more spend would be wasteful).

**Reading response curves:**
- **Steep curves** - High marginal returns (additional spend is very effective). The channel is likely under-invested and has room to grow.
- **Flat curves** - Saturation reached (additional spend has little impact). The channel is at or past its optimal investment level.
- **S-curves** - Typical pattern showing initial ramp-up, peak efficiency, then saturation. Most channels follow this pattern.

The x-axis represents spend level, and the y-axis represents the incremental impact on your KPI. A steeper slope at your current spend level means each additional dollar drives more impact.

<!-- SCREENSHOT: Response curve chart example showing S-curve with annotations for under-invested, optimal, and saturated regions -->

For more detail, see [Glossary: Response Curves](../glossary#response-curves).

## Interpreting Insights

### Media Contribution vs. Spend

Media contribution shows the **true incremental impact** of your media, not just the spend. This concept is also known as **incrementality** - it measures what wouldn't have happened without the media investment.

For example, if you spent $100,000 on TV advertising and it drove 5,000 additional transactions that wouldn't have occurred otherwise, those 5,000 transactions are the incremental contribution. This is different from total transactions, which includes baseline business that would happen anyway.

**Understanding the patterns:**
- **High spend, low contribution** - Oversaturated (past the point of efficiency). You're spending a lot but getting diminishing returns. Consider reducing investment here.
- **Low spend, high contribution** - Efficient (good opportunity for growth). Each dollar is highly effective. Consider increasing investment here.
- **Balanced** - Spending at an optimal level. Contribution is proportional to spend, suggesting you're in the sweet spot.

By comparing spend share to contribution share (e.g., 20% of spend driving 30% of contribution), you can identify over- and under-invested channels.

For more on this concept, see [Glossary: Incrementality](../glossary#incrementality--contribution).

### Cost Efficiency Metrics

Cost efficiency metrics (e.g., cost per visit) help you compare channels on a normalized basis:

- **Lower cost per KPI** = More efficient
- **Higher cost per KPI** = Less efficient

Keep in mind that efficiency alone doesn't tell the whole story—scale and total contribution matter too.

## Common Use Cases

### Scenario 1: Post-Campaign Analysis
**Goal:** Understand what drove results in the last quarter

1. Navigate to **Geographic Insights > Global Meta-Analysis**
2. Review total contribution by market and channel
3. Drill down to **Market Analysis** for specific regions of interest
4. Check **Touchpoint Analysis** to understand channel-level performance

### Scenario 2: Market Comparison
**Goal:** Understand why one market outperforms another

1. Go to **Market Analysis** and select first market
2. Note spend levels and contribution by channel
3. Switch to second market and compare
4. Use **Touchpoint Analysis** to see if specific channels behave differently

### Scenario 3: Channel Strategy Review
**Goal:** Decide whether to expand or reduce a channel

1. Go to **Touchpoint Analysis** and select the channel
2. Review response curves across markets
3. Check if the channel is saturated (flat curve) or has room to grow (steep curve)
4. Compare cost efficiency across markets
5. Use insights to inform [Scenario Planning](../scenario-planning) decisions

## Key Metrics Explained

| Metric | What It Means | How to Use It |
|--------|---------------|---------------|
| **Media Contribution** | Incremental KPI driven by media (e.g., additional transactions) | Compare channels and markets to understand what's driving results |
| **Spend** | Total media investment | Context for contribution (high contribution but also high spend?) |
| **Cost per KPI** | Spend divided by incremental KPI | Efficiency metric for comparing channels on a normalized basis |
| **Effect Share** | Percentage of total media effect from this channel/market | Understand relative importance of each channel |
| **Spend Share** | Percentage of total spend on this channel/market | Compare to effect share to identify over/under-investment |