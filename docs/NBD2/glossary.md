---
title: Glossary
parent: NBD2
nav_order: 4
last_modified_date: 2026-02-23 12:00
---

![Last Revised](https://img.shields.io/badge/last%20revised-2026--02--19-blue?style=flat-square)

# Glossary

Quick reference for key concepts used in NBD. Each entry has a plain-English summary and, where relevant, a Technical Detail section with formulas and worked examples.

**Table of Contents**
* TOC
{:toc}

## Adstock

Adstock models how advertising impact persists beyond the initial exposure, capturing the carry-over effect where an ad seen today continues to influence behavior days or weeks later. Channels like TV typically have higher adstock (longer memory) while performance channels like paid search have lower adstock (immediate impact only).

### Technical Detail

#### Geometric Adstock


```
adstocked_t = spend_t + θ × adstocked_{t-1}
```

Where:

- `spend_t` = Current week's spend
- `θ` = Decay rate (0-1)
- `adstocked_{t-1}` = Previous week's adstocked value

**Interpretation:**

- `θ = 0`: No carry-over (instant decay)
- `θ = 0.5`: Half-life of 1 week
- `θ = 0.9`: Long carry-over (slow decay)

#### Weibull Adstock

More flexible S-shaped decay curve.


#### Impact on Optimization

- **Channels with high adstock** benefit from sustained investment (building momentum)
- **Channels with low adstock** require consistent weekly spend (no momentum)

NBD accounts for adstock when calculating response curves, ensuring realistic predictions. Adstocks are modelled per channel in the MMM model that supports NBD.

## Benchmarks

Benchmarks provide comparison points to assess whether an optimised plan performs better than historical or default spending patterns.


### Benchmark Types

#### 1. Default Benchmark

**What it is:** Average weekly spend × number of weeks

**Purpose:** "Business as usual" baseline

**Example:**

- Historical avg: Google £1k/week, Facebook £800/week
- Plan duration: 4 weeks
- **Benchmark:** Google £4k total, Facebook £3.2k total

**Interpretation:**

- **Large uplift (>15%):** Optimization adds significant value
- **Small uplift (<5%):** Historical spend was already balanced

#### 2. Historical Benchmark

**What it is:** Actual spend from same period last year

**Purpose:** Year-over-year comparison

**Example:**

- Date range: 2026-01-01 to 2026-03-31
- **Benchmark:** Actual spend from 2025-01-01 to 2025-03-31

**Interpretation:**

- **Uplift shows:** How much better this optimised plan is vs. last year
- **Note:** Uplift can be large if historical plans weren't optimised

#### 3. Channel Spend Mix Benchmark

**What it is:** Historical channel allocation scaled to new budget

**Purpose:** Show value of optimised allocation

**Example:**

- Historical: Google 40%, Facebook 30%, TV 30% (£100k total)
- New budget: £150k
- **Benchmark:** Google £60k, Facebook £45k, TV £45k

**Interpretation:**

- **Uplift shows:** Value of reallocation vs. just scaling historical mix

### Comparison Metrics

**KPI Uplift**

```
KPI Uplift = Optimised KPI - Benchmark KPI
```

**KPI Uplift Percent**

```
KPI Uplift % = (KPI Uplift / Benchmark KPI) × 100
```

### Choosing the Right Benchmark

| Scenario | Best Benchmark | Why |
|----------|---------------|-----|
| Annual planning | Historical | YoY comparison |
| Budget increase/decrease | Channel Spend Mix | Shows allocation value |
| General optimization | Default | Shows value vs. BAU |

### Interpreting Results

**Large Uplift (>20%)**

**Indicates:**

- Historical plan was suboptimal
- Significant saturation in some channels
- Underspending in high-ROI channels

**Example:** Over-invested in saturated TV, under-invested in efficient digital

**Medium Uplift (10-20%)**

**Indicates:**

- Room for improvement
- Some channels undersaturated
- Optimization provides clear value

**Typical for:** Well-managed accounts with some inefficiencies

**Small Uplift (<10%)**

**Indicates:**

- Historical plan already well-optimised
- Channels balanced
- Limited room for improvement

**Typical for:** Mature, data-driven accounts

### Benchmark Limitations

**Not a Guarantee**

Benchmarks predict outcomes based on MMM models. Actual results may vary due to:

- Market conditions changing
- Competitor activity
- External factors (economy, trends)

**Historical Context Matters**

Historical benchmark may be artificially high/low if:

- One-time events (Olympics, pandemic)
- Major product launches
- Structural market changes

## Channel

A media channel is a specific platform or medium through which advertising is delivered (e.g., Google Search, Facebook, TV, Display). NBD optimises budget allocation across channels to maximise overall KPI performance.

## Constraints

Constraints ensure optimization stays within realistic and achievable spend limits, preventing recommendations like unrealistic spikes (£50k/week when channel capacity is £5k/week) or dramatic shifts (10x spend increase versus historical). Constraints keep plans realistic, executable, and aligned with business reality.

### Constraint Types

#### 1. Channel Boundary

**What it is:** Min/max total spend per channel across the entire plan

**Purpose:** Ensure spend stays within realistic range vs. historical

**Default calculation:**

```
Historical avg = £10,000/week

Risk Level 3 (±30%):
  Min = £10,000 × 0.70 = £7,000/week
  Max = £10,000 × 1.30 = £13,000/week

For 4 weeks:
  Min total = £28,000
  Max total = £52,000
```

**User override:** Can manually set min/max for specific channels

**Use case:** Lock booked spend, exclude channels, force minimum investment

#### 2. Weekly Boundary

**What it is:** Max spend per week per channel

**Purpose:** Prevent unrealistic week-to-week spikes

**Default calculation:**

```
Historical max weekly spend = £2,000

Weekly boundary = £2,000 × 1.30 = £2,600
```

**Why +30%?** Response curves are modeled on historical data. Spend far beyond historical max produces unreliable predictions.

**Not user-configurable:** Set automatically to ensure model validity

#### 3. Regional Boundary

**What it is:** Min/max total spend per market

**Purpose:** Enforce market-level budget allocations

**Default:** None (optimization can allocate freely across markets)

**User override:** Can set min/max per market

**Use case:** Pre-allocated market budgets, regional strategy requirements

**Example:**

```
Total budget: £10M
UK: Min £5M, Max £7M
US: Min £3M, Max £5M
```

#### 4. Temporal Constraint (Optimise Only)

**What it is:** Spend can only move ±2 weeks from original timing

**Purpose:** Preserve campaign timing and domain knowledge

**Applies to:** Optimise existing plan (not generate)

**Why:** The original plan may contain timing insights not captured in historical data:

- Product launches
- Seasonal campaigns
- Competitive response

**Example:**

Original plan has £10k in Week 3 for Google Search.

Optimised plan can move this to:

- Week 1 ✓
- Week 2 ✓
- Week 3 ✓
- Week 4 ✓
- Week 5 ✓
- Week 6 ✗ (too far)

### Risk Level and Flexibility

Risk level (1-5) controls channel boundary flexibility:

| Risk | Flexibility | Min/Max vs. Historical |
|------|-------------|------------------------|
| 1 | Conservative | ±15% |
| 2 | Cautious | ±20% |
| 3 | Balanced | ±30% (default) |
| 4 | Aggressive | ±40% |
| 5 | Very Aggressive | ±50% |

**Higher risk = wider boundaries = more room to reallocate**

### Common Use Cases

#### Lock a Channel

**Scenario:** Spend already booked, cannot change

**Solution:**

```json
{"min": 500000, "max": 500000}
```

#### Exclude a Channel

**Scenario:** Don't want to spend on this channel

**Solution:**

```json
{"min": 0, "max": 0}
```

#### Force Minimum Investment

**Scenario:** Must spend at least X on brand channels

**Solution:**

```json
{"min": 1000000, "max": 5000000}
```

#### Market Budget Splits

**Scenario:** UK gets 60%, US gets 40% of budget

**Solution:**

```json
{
  "regional_boundary": {
    "uk": {"min": 5500000, "max": 6500000},
    "us": {"min": 3500000, "max": 4500000}
  }
}
```

### When Constraints Fail

**Impossible to Satisfy**

- **Error:** "Channel minimums exceed budget"
- **Cause:** Sum of all min constraints > total budget
- **Solution:** Reduce mins or increase budget

**Over-Constrained**

- **Error:** "Channel maximums below budget"
- **Cause:** Sum of all max constraints < total budget
- **Solution:** Increase maxs or reduce budget

**Conflicting Regional + Channel**

- **Error:** "Cannot satisfy both regional and channel constraints"
- **Cause:** Channel constraints don't allow regional allocation
- **Solution:** Adjust constraints to be compatible

## Contribution

Contribution is the portion of total KPI attributed to media, showing what share of business outcomes came from each channel. It differs from spend share: a channel with 50% of budget might drive 60% of media contribution (efficient) or only 40% (inefficient). See Incrementality & Contribution for more details.

## Incrementality & Contribution

Incrementality is the true causal impact of media—what would NOT have happened without the media spend. Contribution is the portion of total KPI attributed to media. Together, these concepts separate correlation from causation and guide optimization based on actual business value, not impressions or spend.

### Incrementality

**What It Means**

Incrementality answers: "How many additional transactions did this media drive?"

**Not:**
- Correlation (media and sales both up)
- Attribution (last-click credit)

**But:**
- Causation (media caused sales)

**Example:**

- **Total transactions:** 10,000
- **Baseline (no media):** 7,000
- **Incremental (from media):** 3,000

Media incrementality = 3,000 transactions

### Contribution

**What It Means**

Contribution is the share of total KPI driven by each component:

```
Total KPI = Media Contribution + Baseline + Seasonal + Other Factors
```

**Example:**

- Media contribution: 30%
- Baseline: 50%
- Seasonal: 15%
- Other: 5%

**Media Contribution Breakdown**

Within media contribution, each channel contributes:

```
Total Media = Google Search + Facebook + TV + ... + Other Channels
```

### Contribution vs. Spend

Key insight: **Contribution ≠ Spend**

**Example:**

| Channel | Spend | Spend Share | Contribution | Effect Share |
|---------|-------|-------------|--------------|--------------|
| Google Search | £50k | 50% | 8,000 txns | 60% |
| TV | £50k | 50% | 5,333 txns | 40% |

**Interpretation:**

- Google Search is **more efficient** (60% effect from 50% spend)
- TV is **less efficient** (40% effect from 50% spend)

This guides optimisation: **increase Google, reduce TV**.

### Measuring Incrementality

MMM estimates incrementality by:

1. **Historical analysis** - Compare weeks with high/low spend
2. **Controlling for confounders** - Account for seasonality, promotions, trends
3. **Statistical modeling** - Isolate media effect from noise

**Output:** Response curves showing incremental KPI per spend level.

### Why It Matters for NBD

NBD optimises based on **incremental contribution**, not spend or impressions.

**Bad optimization:** Maximise impressions

**Good optimization:** Maximise incremental KPI

This ensures every dollar drives the most possible business value.

## KPI

KPI (Key Performance Indicator) is the business outcome you want to maximise through media optimization. Common KPIs include transactions, revenue, new customer acquisitions, or leads. NBD optimises media plans to deliver the maximum predicted KPI within budget and constraints.

## Market

A market refers to a geographic region or business unit (e.g., UK, US, France) where media campaigns run. NBD can optimise across multiple markets simultaneously, subject to regional boundary constraints if specified.

## Nested Models

Nested models refer to NBD's approach of running separate MMM models for each market when optimising multi-market plans. Each market has its own response curves, seasonality patterns, and baseline performance, which are combined at the portfolio level to calculate total predicted KPI.

### Scaler Calculation

When combining markets, NBD uses scalers to normalise predictions:

```
market_scaler = market_historical_average_kpi / robyn_predicted_average_kpi
```

This ensures model predictions align with actual market performance.

### Seasonality

Each market's model captures its own seasonal patterns:

- UK may have Christmas peak in December
- US may have Thanksgiving peak in November
- Southern hemisphere markets may have reversed seasonal patterns

### Direct vs. Indirect Contribution

- **Direct contribution:** KPI driven by media in that specific market
- **Indirect contribution:** Spillover effects (e.g., national TV affecting multiple markets)

NBD primarily optimises for direct contribution, though cross-market effects can be modeled if data supports it.

## Reinforcement Learning

Reinforcement Learning (RL) is the algorithm NBD uses to allocate budget optimally across channels and weeks. It works iteratively, testing which channel would benefit most from the next increment of budget, then allocating accordingly, repeating until the full budget is distributed. This approach handles complex constraints and nonlinear response curves effectively.

### Why Reinforcement Learning?

Budget optimization is a complex problem:

- **Many channels** (10-20+)
- **Many weeks** (4-52)
- **Nonlinear response curves** (diminishing returns)
- **Multiple constraints** (channel, weekly, regional, temporal)
- **Massive search space** (billions of possible allocations)

RL provides:

- **Flexibility** in adding custom constraints
- **Interpretability** (each step is explainable)
- **Adaptability** to external factors (seasonality, profit margins)
- **Client-specific configuration**

### RL Components

**State**

Current budget allocation across all channels:

```python
state = {
    "google_search_uk": 45000,  # Current allocated
    "facebook_uk": 32000,
    "tv_uk": 80000,
    ...
}
```

**Action**

Allocate an increment (£2,000) to a specific channel:

```python
action = ("google_search_uk", increment=2000)
```

**Reward**

Predicted incremental KPI from this action:

```python
reward = response_curve.predict(new_spend) - response_curve.predict(old_spend)
```

**Example:** Adding £2,000 to Google Search predicts +12.5 transactions

**Policy**

How to select actions: **ε-greedy**

- **Exploration (ε=0.03):** 3% of the time, choose random channel
- **Exploitation (1-ε=0.97):** 97% of the time, choose best channel

### Algorithm Pseudocode

```
1. Initialise: Set all channels to minimum spend
2. While total_allocated < budget:
    a. For each available channel:
       - Simulate adding increment
       - Calculate reward (incremental KPI)
       - Store reward
    b. Select action:
       - With probability ε: choose random channel (explore)
       - With probability 1-ε: choose best channel (exploit)
    c. Apply action:
       - Allocate increment to selected channel
       - Update state
    d. Check constraints:
       - If channel hit max boundary, remove from available
3. Distribute weekly: Spread total channel spend across weeks
4. Return optimised plan
```

### Example Walkthrough

**Setup**

- **Budget:** £100,000
- **Channels:** Google Search (GS), Facebook (FB), TV
- **Increment:** £2,000
- **ε:** 0.03
- **Constraints:** GS max £40k, FB max £30k, TV max £30k

**Iteration 1**

**State:** GS=£0, FB=£0, TV=£0 (all at minimum)

**Simulate:**

- GS +£2k → Reward = 15.2 txns
- FB +£2k → Reward = 14.8 txns
- TV +£2k → Reward = 12.1 txns

**Select:** GS (best reward)

**New State:** GS=£2,000, FB=£0, TV=£0

**Iteration 2**

**Simulate:**

- GS +£2k → Reward = 15.1 txns (slightly lower, approaching saturation)
- FB +£2k → Reward = 14.8 txns
- TV +£2k → Reward = 12.1 txns

**Select:** GS (still best)

**New State:** GS=£4,000, FB=£0, TV=£0

**... (Iterations 3-19)**

GS continues to be best until it approaches saturation or hits max boundary.

**Iteration 20**

**State:** GS=£38,000 (near max)

**Simulate:**

- GS +£2k → Reward = 3.2 txns (saturated)
- FB +£2k → Reward = 14.8 txns
- TV +£2k → Reward = 12.1 txns

**Select:** FB (now best)

**New State:** GS=£40,000 (max), FB=£2,000, TV=£0

**Iteration 21+**

FB receives allocations until it saturates or maxes out, then TV receives remainder.

**Final State**

GS=£40,000, FB=£30,000, TV=£30,000 (all at max, £100k allocated)

### Why ε-Greedy?

**Pure exploitation (ε=0):** Might miss better solutions due to early saturation

**Pure exploration (ε=1):** Random, no learning

**ε-greedy (ε=0.03):** Mostly exploits best channel, but occasionally explores others to avoid local optima

### Response Curves in RL

Each action's reward comes from the response curve.

The reward for each action is the difference in response curve output between the current spend and spend + increment — i.e., the marginal KPI gain from adding one increment to that channel.

Response curve includes:

1. **Adstock** (carry-over)
2. **Saturation** (diminishing returns)

See Response Curves for details.

### Constraints in RL

Before selecting an action, channels that have hit their max boundary or weekly cap are excluded. The best action is then chosen from the remaining available channels.

See Constraints for constraint types.

### Advantages of RL for NBD

| Feature | Benefit |
|---------|---------|
| **Iterative** | Can stop early if needed, partial results valid |
| **Explainable** | Each step shows why allocation was made |
| **Flexible** | Easy to add new constraint types |
| **Robust** | Handles irregular response curves gracefully |
| **Scalable** | Works for 5 or 50 channels |

### Limitations

- **Slow for huge search spaces** (50+ channels × 52 weeks)
- **No global optimality guarantee** (local optimum possible)
- **Sensitive to increment size** (too large = coarse, too small = slow)

**Mitigations:**

- Use reasonable increment (£2,000 typical)
- Run for sufficient iterations (50k-200k)
- ε-greedy helps escape local optima

## Response Curves

Response curves show how incremental media spend translates to incremental KPI contribution, capturing the principle of diminishing returns. As you increase spend in a channel, each additional dollar produces less incremental impact than the previous dollar due to saturation (e.g., first £10k on Google Search might generate 500 transactions, next £10k might only generate 300 more).

### Hill Saturation Function

Robyn uses the Hill equation (S-curve):

```
response = α × (spend^γ) / (K^γ + spend^γ)
```

Where:

- `α` = Maximum possible response (asymptote)
- `γ` = Shape parameter (steepness)
- `K` = Inflection point (50% saturation spend level)

### Three Regions

**1. Ramp-Up (Low Spend)**

- **Behavior:** Steep gains, high marginal returns
- **Why:** Building awareness, reaching new audience
- **Action:** Increase spend

**2. Optimal Zone (Medium Spend)**

- **Behavior:** Strong returns, approaching diminishing
- **Why:** Reaching target audience efficiently
- **Action:** Maintain or slightly increase

**3. Saturation (High Spend)**

- **Behavior:** Flat curve, low marginal returns
- **Why:** Over-exposing audience, wasted impressions
- **Action:** Reduce spend, reallocate to other channels

### Visual Example

```
Response
   │
 α ├─────────────────────────── (saturation)
   │               ╱─
   │            ╱─
   │         ╱─
   │      ╱─
   │   ╱─
   │╱─
   └────────────────────────> Spend
   0         K              High
```

### Why It Matters for NBD

NBD uses response curves to:

1. **Predict KPI** for any spend level
2. **Find optimal allocation** across channels
3. **Avoid over-saturating** channels

Optimization stops adding spend to a channel once it hits the flat part of the curve.

### Combining with Adstock

Full response calculation:

```
1. Apply adstock transformation → adstocked_spend
2. Apply Hill saturation → response
3. Sum across channels and weeks → total KPI
```

See Adstock for details on step 1.

## Risk Level

Risk level (1-5) controls how much budget allocation can deviate from historical patterns, with higher risk levels allowing more aggressive reallocation. It affects channel boundary constraints, where Risk Level 1 (Conservative) allows ±15% deviation and Risk Level 5 (Very Aggressive) allows ±50% deviation from historical averages.

| Risk | Flexibility | Min/Max vs. Historical |
|------|-------------|------------------------|
| 1 | Conservative | ±15% |
| 2 | Cautious | ±20% |
| 3 | Balanced | ±30% (default) |
| 4 | Aggressive | ±40% |
| 5 | Very Aggressive | ±50% |

**Example Calculation (Risk Level 3):**

```
Historical avg = £10,000/week

Min = £10,000 × 0.70 = £7,000/week
Max = £10,000 × 1.30 = £13,000/week

For 4 weeks:
  Min total = £28,000
  Max total = £52,000
```

**Higher risk = wider boundaries = more room to reallocate**

## Robyn

Robyn is Meta's open-source Marketing Mix Modeling (MMM) framework and the engine that generates the response curves and decompositions NBD uses for optimization. Robyn trains MMM models using historical data, estimates adstock and saturation parameters for each channel, and decomposes KPI into media, baseline, seasonal, and other factors.

### What Robyn Does

1. **Trains MMM models** using historical data (spend + KPI + context)
2. **Estimates adstock and saturation** parameters for each channel
3. **Decomposes KPI** into media, baseline, seasonal, and other factors
4. **Outputs response curves** showing spend vs. incremental KPI

### Key Components

**Ridge Regression**

Statistical method for estimating coefficients with regularization (prevents overfitting).

**Adstock Transformations**

Models carry-over effects. See Adstock.

**Saturation Curves**

Models diminishing returns. See Response Curves.

**Hyperparameter Optimization**

Uses Nevergrad (evolutionary algorithm) to search for best adstock/saturation parameters.

**Result:** Hundreds of models on the Pareto frontier (trade-offs between fit, business logic, and parsimony).

### Robyn Workflow

```
Historical Data (spend, KPI, context)
    ↓
Robyn Training
    ↓
Nevergrad Optimization (2000+ iterations)
    ↓
Pareto Frontier (500+ models)
    ↓
Model Selection (choose best)
    ↓
Outputs (pareto_*.csv)
    ↓
NBD (reads outputs for optimization)
```

### Outputs

Robyn generates three key files used by NBD:

1. **pareto_aggregated.csv** - Channel metrics (ROI, contribution, spend share)
2. **pareto_hyperparameters.csv** - Response curve parameters (α, γ, θ)
3. **pareto_alldecomp_matrix.csv** - Weekly time series decomposition

### Why Robyn?

**Strengths:**

- Open-source, well-documented
- Handles adstock and saturation automatically
- Fast hyperparameter optimization
- Active community and development

**NBD's Use Case:**

- Robyn provides the **"what happened?"** (historical decomposition)
- NBD adds the **"what should we do?"** (forward-looking optimization)

## Share Code

A share code is a unique identifier that allows users to share and access saved scenarios within NBD. When you save a scenario, a share code is generated that can be used to reload that exact configuration, including budget, constraints, date ranges, and optimization results.
