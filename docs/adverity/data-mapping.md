---
title: Data Mapping
parent: Adverity
nav_order: 6
last_modified_date: 2025-01-23 12:00
---

# Data Mapping

Data mapping ensures that column names are standardized across datastreams for consistency and clarity.  

## General Guidelines  

1. **Dimension Naming**:  
   - Use `_name` as a suffix for dimension columns.  
     Example:  
     ```
     campaign_name, placement_adset_name, platform_name
     ```  

2. **Metric Naming**:  
   - Use full, descriptive names for metrics.  
   - Metrics should be **pluralised** (e.g., `impressions`, `clicks`) and avoid abbreviations.  
     Example:  
     ```
     impressions, clicks, conversions
     ```  

3. **Avoid Ambiguity**:  
   - Ensure column names are clear and unambiguous. Avoid shortened or inconsistent terms.  

4. **Consistency**:  
   - Align column names with existing datastreams for uniformity. ie. placement_adset_name for placement, adgroup, adset dimensions. 


{: .important}
Refer `Datastream-ETL` repo - the `COMMON_COLUMN_RENAME` mapping within the `etl/constants.py` file, which highlights and corrects frequent misnames. Ensure you are using the corrected names as much as possible

