---
title: Gold Parsed Tables
parent: Taxonomy Checker
nav_order: 6
last_modified_date: 2025-01-27 12:00
---

# Gold Parsed Tables

## Overview

The gold tables have been fleshed out completely for New Balance and Value Retail in the `New Balance - Gold Table` and `Value Retail - Gold Table` notebooks. 

The bulk of the work for this happens in trying to map the schemas and the taxonomy definitions.

Part of the New Balance on Can be seen below. 

```
TAXONOMY_DEFINITION: Final[Dict[str, Dict[str, Dict[str, str]]]] = {
    "Search Campaign": {
        "TX2": {
            "chunk1": "taxonomy_version",
            "chunk2": "brand",
            "chunk3": "market",
            "chunk4": "channel_name",
            "chunk5": "platform",
            "chunk6": "campaign_objective",
            "chunk7": "category",
            "chunk8": "tactic",
            "chunk9": "match_type",
            "chunk10": "product",
            "chunk11": "campaign_freeform",
        },
        "TX3": {
            "chunk1": "taxonomy_version",
            "chunk2": "market",
            "chunk3": "time_period",
            "chunk4": "channel_name",
            "chunk5": "platform",
            "chunk6": "funnel",
            "chunk7": "tactic",
            "chunk8": "budget_name",
            "chunk9": "category",
            "chunk10": "campaign_objective",
            "chunk11": "campaign_freeform",
        },
    },
```

This is taking the various versions of the taxonomy and assigning the chunks to headers. 
Keep consistency with the headers they will be assigned as column headers in your tables.

The schema file in the parsed client folders show the parsed naming convention table schemas for each channel you are checking. 

There idea would be to include all the available columns for all the versions of the taxonomy per channel. 

For the above this looks like:

```

search_campaign_schema = StructType(
    [
        StructField("advertiser_id", LongType(), True),
        StructField("account_id", LongType(), True),
        StructField("campaign_id", LongType(), True),
        StructField("advertiser_name", StringType(), True),
        StructField("day", DateType(), True),
        StructField("campaign_name", StringType(), True),
        StructField("taxonomy_version", StringType(), True),
        StructField("brand", StringType(), True),
        StructField("market", StringType(), True),
        StructField("channel_name", StringType(), True),
        StructField("time_period", StringType(), True),
        StructField("platform", StringType(), True),
        StructField("campaign_objective", StringType(), True),
        StructField("budget_name", StringType(), True),
        StructField("category", StringType(), True),
        StructField("tactic", StringType(), True),
        StructField("match_type", StringType(), True),
        StructField("product", StringType(), True),
        StructField("campaign_freeform", StringType(), True),
    ]
)
```

You may wish to unify this across granularities as over the different versions you will find null values for taxonomy structures that have not been followed. 

