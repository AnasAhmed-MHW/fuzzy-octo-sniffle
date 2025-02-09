---
title: New Client Guide
parent: Analyst Engineering Guide
nav_order: 10
last_modified_date: 2025-01-23 12:00
---

# New Client Guide

This guide outlines the essential steps and considerations for onboarding a new client, ensuring seamless integration with SIGNAL and analytics workflows.

## Overview

The primary goal is to understand the platforms, accounts, metrics, and breakdowns required for visualisation and analytics.

## SIGNAL Connector Sheet

We have created a [Google Sheet](https://docs.google.com/spreadsheets/d/1ttLu_d2DCYATU6RNwSr49q8BejNmOscDJRPFkClLCY0) to help document the platforms and connections needed. This sheet follows a structured framework with the following key headers:

### Client Input Fields
- **Media Platform**: Name of the platform to connect (e.g., Meta, Google Ads, Campaign Manager).
- **Market**: Countries the platform/account is connected to.
- **Channel**: Media channel associated with the activity (e.g., Social, Search, OLV).
- **Has Activity in Previous Year [YYYY]?**: Indicates if the platform had activity in the past year (helps determine historical data needs).
- **Priority (1-5, 1 highest)**: Importance of this channel.
- **Number of Accounts**: Active accounts within this platform.
- **All investment included in media plan?**: Specifies whether all media investment is tracked in MediaPlans (Y/N).
- **Account ID / Name / Identifier**: List of account IDs or advertiser IDs for debugging.
- **Platform Authorisation Owner / Contact Email**: Contact responsible for granting API access.

### Engineer Input Fields
- **Adverity Authorisation to be Used / Given**: Email address for API access (typically `adtech.analytics@mediahubww.com`).
- **Month / Year Auth Given**: When authorisation was granted (important for monitoring expiration dates).
- **Authorisation Status**: Ongoing status tracking.
- **Additional Notes**: Any extra details or special considerations.

## Nuances & Special Considerations

While we follow standard platform breakdowns, some clients may have specific requirements. Speak with an engineer if any of the following apply:

- **Geo Breakdowns**: Some platforms do not provide complete geo-segmented data, requiring additional processing.
- **Reach / Frequency Reports**: These are often aggregate-level reports and may not support time series breakdowns.
- **Custom Metrics & Attribution**: Ensure tracking aligns with media delivery granularity.
- **Planned vs. Actualised Data**: Understanding how planned investments align with real-time reporting.
- **Google Trends**: Not included in the standard SIGNAL setup.
- **Custom DSP Reports & Data Appending**: Additional configurations may be required.
- **Untracked DSP Campaigns**: Campaigns not tracked in CM may need manual intervention.
- **Non-Standard DSPs (e.g., Yahoo, TheTradeDesk, Teads, Hawk, DV360)**: These may not follow the standard Kinesso structure and require custom logic.

{: .warning}
If conversions are tracked at a different granularity than media delivery, inconsistencies in reporting will arise. Ensure tracking is aligned at the same granularity level.

## Setup Process

### 1. Taxonomy Section
Ensures standardisation of naming conventions, tracking methodologies, and categorisations.
This will reuire datastream and taxonomy checker configurations to ensure the naming categorisation is done correctly. 

For Taxonomy we will need to have:
- A master list of approved headers and the values alongside this
- Structure of taxonomy - ie Taxonomy Version, Brand, Country, Channel etc.

This can also be worked out from a Naming Convention Template. 

### 2. SIGNAL Pipeline
For each platform the SIGNAL pipeline may consist of two key sections:

#### a) Media Delivery
Captures impressions, clicks, costs, video views, and other delivery-related metrics.

#### b) Media Conversions
Tracks user events, which vary by client and platform. These may include likes, add-to-cart actions, purchases, footfall, revenue, or signups. Measurement depends on tracking configurations within the platform.

There are some platforms were the media delivery and the media conversions can be fetched in one datastream (ie Meta).

*Conversions are standardised to be fetched from corresponding platforms for consistency.*

## How Timelines Are Affected

Timelines may be impacted by added complexities, such as:

- **Geo Breakdowns**: Some platforms require schema adjustments or duplicate data streams.
- **Reach / Frequency Reports**: Some platforms lack accurate reporting, requiring custom data processing.
- **Cross-Platform Conversions**: Aligning conversions from external sources (e.g., Google Analytics) with media delivery data adds complexity.
- **Custom DSP Integrations**: Additional connectors and logic may extend timelines.

## Scale Considerations

Understanding the scale of the client’s operations is crucial. Factors to assess:
- **Number of Accounts & Markets**: Differences in account structures and naming conventions across regions may add complexity.
- **Multi-Agency Collaboration**: Larger clients may have multiple agencies handling different regions or platforms.

## Dashboard Planning

Before implementation, outline a wireframe of expected dashboards:
- Define **gold tables** and how they should be structured.
- Identify the necessary **granularity of summary tables**.
- Consider any **specialist views** required per channel.

### Missing Elements & Recommendations
- **API Rate Limits**: Considerations for API rate limitations affecting data retrieval.
- **Historical Data Strategy**: Clear guidelines on how far back data should be pulled.
- **Automated Monitoring & Alerts**: Set up proactive notifications for API failures or data inconsistencies.
- **Data Retention Policies**: Define how long data is stored and archived.

By addressing these factors early, onboarding can be streamlined, ensuring accurate and reliable reporting for new clients.

