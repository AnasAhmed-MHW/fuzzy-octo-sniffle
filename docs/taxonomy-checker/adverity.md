---
title: Adverity
parent: Taxonomy Checker
nav_order: 2
last_modified_date: 2025-01-20 12:00
---

# Adverity Datastream Configuration

---

## Objective

The Adverity naming convention datastreams must be configured to avoid timeseries breakdowns. Instead, the focus should be on fetching **relevant and up-to-date dimensions** (e.g., campaign, placement, ad) and their associated IDs. This ensures that the data pipeline provides the most recent and accurate information for taxonomy validation.

### Key Goals:
1. **Fetch the Most Recent Version**: Ensure the datastream retrieves the latest dimension names and IDs.
2. **Avoid Timeseries Breakdowns**: Do not include date-based breakdowns at this stage of the pipeline.
3. **Maintain Consistency**: Use consistent naming conventions that align with platform-specific configurations and schemas.

---

## Configuration Guidelines

To achieve the objectives outlined above, follow these guidelines when configuring Adverity datastreams:

### 1. **Focus on Relevant Dimensions**
   - Ensure the datastream fetches only the most relevant dimensions, such as:
     - Campaign names and IDs
     - Placement names and IDs
     - Ad names and IDs

### 2. **Fetch the Latest Data**
   - Configure the datastream to retrieve the **most recent version** of dimension names and IDs.
   - This ensures that the taxonomy checker uses up-to-date information for validation.

### 3. **Avoid Timeseries Breakdowns**
   - Do not include date-based breakdowns (e.g., daily, weekly, or monthly splits) in the datastream.
   - Timeseries data should be handled at a later stage of the pipeline, if needed.

### 4. **Use Consistent Naming Conventions**
   - Align naming conventions with platform-specific configurations and schemas.
   - Ensure consistency across all datastreams to avoid confusion and errors.

---

- **Fields to Include**:
  - `campaign_id`
  - `campaign_name`
  - `account_id`
  - `account_name`
  - `advertiser_id`
  - `advertiser_name`

these will help build the breadcrumbs for joining the data back to the SIGNAL pipeline. 