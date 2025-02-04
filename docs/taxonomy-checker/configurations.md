---
title: Configurations
parent: Taxonomy Checker
nav_order: 2
last_modified_date: 2025-01-27 12:00
---

# Taxonomy Configurations

The configurations for the Taxonomy Checker are defined in the `/client_config_constant.py` file. This file contains a variable called `CLIENT_DICT`, which stores client-specific settings. When adding a new client, you must append their configuration to this dictionary.

Below is an example configuration for a client named "Value Retail":

```python
"Value Retail": { 
    "CLIENT": "value_retail",
    "SHEET_ID": "1rYsIpscgFCDN_YX6TnDEp9ZCfm_C8O_CZ1pZNv25n04",
    "AWS_BUCKET": "mh-valueretail-adverity-rawdata",
    "AVAILABLE_CHANNELS": ["meta", "google", "campaignmanager", "tiktok", "linkedin"],
    "MANUAL_TABLE": "raw.new_balance.bronze_manualinput_namingconv",
    "MANUAL_JOINS": {
        "hive_metastore.new_balance.silver_thetradedesk_creative": "thetradedesk",
        "hive_metastore.new_balance.silver_silverpush": "silverpush",
        "hive_metastore.new_balance.silver_reddit_reporting": "reddit"
    },
    "ACTIVITY_WINDOW": "30",
    "IMPRESSION_THRESHOLD": 10,
    "CAMPAIGN_TABLES": [
        "gold_googleads_campaign_dashboard",
        "silver_meta_reporting",
        "silver_campaignmanager_creative"
    ],
    "AD_TABLES": [
        "silver_googleads_reporting",
        "silver_meta_reporting",
        "silver_campaignmanager_creative"
    ],
    "CHANNEL_TABLES": {
        "meta": "hive_metastore.value_retail.silver_meta_reporting",
        "google": "hive_metastore.value_retail.silver_googleads_reporting",
        "campaignmanager": "hive_metastore.value_retail.silver_campaignmanager_creative",
        "tiktok": "hive_metastore.value_retail.silver_tiktok_country_reporting",
        "linkedin": "hive_metastore.value_retail.gold_linkedin_creative_reporting"
    },
    "DATE_FETCH": "Latest",
    "SUBSTITUTION_SHEET": True,
    "SUBSTITUTION_SHEET_ID": "1m4TUDxEhlw5fqAKqxxS4PttI-6EUanjHtF3kXfnGjU0"
}
```

---

## Configuration Keys and Their Purpose

Below is a detailed explanation of each key in the `CLIENT_DICT` configuration:

### **`CLIENT`**
- **Purpose**: The catalog or schema name for the client. This should match the folder names and remain consistent across all systems.
- **Example**: `"value_retail"`

### **`SHEET_ID`**
- **Purpose**: The Google Sheet ID for the governance document. This is found in the URL of the Google Sheet.
- **Example**: For the URL `https://docs.google.com/spreadsheets/d/1rYsIpscgFCDN_YX6TnDEp9ZCfm_C8O_CZ1pZNv25n04/edit?gid=1900709516#gid=1900709516`, the `SHEET_ID` is `1rYsIpscgFCDN_YX6TnDEp9ZCfm_C8O_CZ1pZNv25n04`.

### **`AWS_BUCKET`**
- **Purpose**: The name of the AWS S3 bucket where raw taxonomy files are stored.
- **Example**: `"mh-valueretail-adverity-rawdata"`

### **`AVAILABLE_CHANNELS`**
- **Purpose**: A list of channels that are categorized in the AWS bucket under the `canonical/name` folder. Each channel should have a corresponding folder (e.g., `s3://bucket-name/canonical/name/googleads`).
- **Example**: `["meta", "google", "campaignmanager", "tiktok", "linkedin"]`

### **`MANUAL_TABLE`**
- **Purpose**: If taxonomy names cannot be fetched through Adverity and stored in the `canonical/name` folder, this key specifies the table from which to fetch the names.
- **Example**: `"raw.new_balance.bronze_manualinput_namingconv"`

### **`MANUAL_JOINS`**
- **Purpose**: A dictionary that maps manual tables to their respective channels. This ensures that only active and live data is used for validation. 
- This value in this dict should match the `source_name` in the bronze manual table. 
- **Example**:
  ```python
  {
      "hive_metastore.new_balance.silver_thetradedesk_creative": "thetradedesk",
      "hive_metastore.new_balance.silver_silverpush": "silverpush",
      "hive_metastore.new_balance.silver_reddit_reporting": "reddit"
  }
  ```

### **`ACTIVITY_WINDOW`**
- **Purpose**: Defines the lookback window for determining active taxonomy values. This can be a number (e.g., `30` days) or a specific date. Any taxonomy values outside this window are considered inactive.
- **Example**: `"30"`
- **Example**: `"2023-01-01"`

### **`IMPRESSION_THRESHOLD`**
- **Purpose**: The minimum number of impressions required for a taxonomy value to be considered active.
- **Example**: `100`

### **`CAMPAIGN_TABLES`**
- **Purpose**: A list of campaign-level tables used to determine if campaigns are active based on the `ACTIVITY_WINDOW` and `IMPRESSION_THRESHOLD`.
- **Example**:
  ```python
  [
      "gold_googleads_campaign_dashboard",
      "silver_meta_reporting",
      "silver_campaignmanager_creative"
  ]
  ```

### **`AD_TABLES`**
- **Purpose**: A list of ad-level tables used to determine if ads are active based on the `ACTIVITY_WINDOW` and `IMPRESSION_THRESHOLD`.
- **Example**:
  ```python
  [
      "silver_googleads_reporting",
      "silver_meta_reporting",
      "silver_campaignmanager_creative"
  ]
  ```

### **`CHANNEL_TABLES`**
- **Purpose**: A dictionary that maps each channel in `AVAILABLE_CHANNELS` to its corresponding table. This helps determine if the channel has active taxonomy values.
- **Example**:
  ```python
  {
      "meta": "hive_metastore.value_retail.silver_meta_reporting",
      "google": "hive_metastore.value_retail.silver_googleads_reporting",
      "campaignmanager": "hive_metastore.value_retail.silver_campaignmanager_creative",
      "tiktok": "hive_metastore.value_retail.silver_tiktok_country_reporting",
      "linkedin": "hive_metastore.value_retail.gold_linkedin_creative_reporting"
  }
  ```

### **`DATE_FETCH`**
- **Purpose**: Specifies the date range for fetching canonical name files. Use `"Latest"` to fetch only the most recent file, or provide a date range for broader fetches.
- **Example**: `"Latest"`

### **`SUBSTITUTION_SHEET`**
- **Purpose**: A boolean value indicating whether a substitution sheet is associated with the client. The substitution sheet allows overriding taxonomy values.
- If this value is True then you will need a value in the `SUBSTITUTION_SHEET_ID`
- **Example**: `True`

### **`SUBSTITUTION_SHEET_ID`**
- **Purpose**: The Google Sheet ID for the substitution sheet. This sheet is typically stored in a separate Google Sheet to facilitate sharing with external teams.
- **Example**: `"1m4TUDxEhlw5fqAKqxxS4PttI-6EUanjHtF3kXfnGjU0"`

