---
title: Dashboard Breakdown
parent: Dashboards
grand_parent: Value Retail
nav_order: 1
last_modified_date: 2026-11-05 10:00
---

# Dashboard Breakdown

Value Retail has 4 Power BI dashboards.

## 1. True Metrics

> <https://app.powerbi.com/groups/80a60f78-2cbd-4879-ad2f-ddbe36ede532/reports/4e3197f4-c1cf-4155-b15c-411f1e904719/ebaf460118eca087bbb7?experience=power-bi&clientSideAuth=0>

**Table Used:** `gold_true_metric`

**Function:** Provides the user with a response from a specific channel towards both Footfall and Sales.

For further detail on how it's built, see the [True Metrics documentation](../true-metrics/).

## 2. Media Investment

> <https://app.powerbi.com/groups/80a60f78-2cbd-4879-ad2f-ddbe36ede532/reports/3607c9bb-2a9d-49b9-9d1f-b067457690a2?experience=power-bi&clientSideAuth=0>

**Table Used:** `hive_metastore.value_retail.gold_mediaplan`

**Function:** Provides users with breakdowns of both Online data from Platforms and Offline data from mediaplans.

For further detail, see the [Mediaplans documentation](../mediaplans/) (Radar → Databricks ingest) and [Media Investment Data](../mmm-data-processing/media-investment-data/) (gold mediaplan, channel mapping, and versioning).

## 3. Digital Performance

> <https://app.powerbi.com/groups/80a60f78-2cbd-4879-ad2f-ddbe36ede532/reports/dcc938fb-3253-47a7-9ca1-5c43dfdb5ae9?experience=power-bi&clientSideAuth=0>

**Table Used:** `hive_metastore.value_retail.gold_allchannel_summary`

**Function:** Provides a detailed breakdown of performance from online platforms. Breaking down data by day/week/month etc and all metrics.

For further detail on the channel-level data pipeline, see [Search, Social and API](../mmm-data-processing/media-investment-data/search-social-and-api/).

## 4. Triple MMM

> <https://app.powerbi.com/groups/80a60f78-2cbd-4879-ad2f-ddbe36ede532/reports/4f4be407-f53e-4ff9-b4ce-9bdb8d9547b5?experience=power-bi&clientSideAuth=0>

**Table Used:** `uc_dev.value_retail.gold_mmm_results_test_ext`

**Function:** Provides a summary of MMM results for clients and local teams to understand impact from media and other marketing activities. Breaks down models by village, channel and audiences. Measures Footfall and Sales as the main metric.

For further detail on how this data is prepared, see the [Dashboarding Phase](../mmm-data-processing/dashboarding-phase/) (MLP → NBD → Delta → Power BI). 