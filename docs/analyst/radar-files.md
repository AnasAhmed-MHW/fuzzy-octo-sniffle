---
title: RADAR Shared Files
parent: Analyst Engineering Guide
nav_order: 2
last_modified_date: 2025-01-23 12:00
---

# RADAR Files

## Where Files Are Stored

Client folders are stored within the `mh-mediaplans` bucket under the `templates` folder.

The `RADAR` app displays _all_ files in the client folder.

## Linking SharePoint and AWS S3

To configure SharePoint and AWS S3, update the `client_config` in the `Sharepoint-to-S3` repository. Append the necessary `config` variables in the dictionary.

Each section of the dictionary includes comments for guidance. For a new client, append a new key to the `config` dictionary following this structure:

```python
config = {
    "client": {
        "site_url": "https://interpublic.sharepoint.com",  # This should remain interpublic
        "files": [  # File paths where the MediaPlan is stored
            "MediahubUKSharedLibrary/Shared Documents/Templates/Media Plan Templates/MHUK_MediaPlan_Master_NewBalance_Template.xlsx",
            "MediahubUKSharedLibrary/Shared Documents/Templates/Media Plan Templates/MHUK_MediaPlan_Master_NewBalance_Template_2024.xlsx",
            "MediahubUKSharedLibrary/Shared Documents/Templates/Ad Ops Templates/Digital Taxonomy Templates/New Balance Global Media Taxonomy 2024.xlsx",
        ],
        "alias": {  # Rename files for better readability in the RADAR app
            "MHUK_MediaPlan_Master_NewBalance_Template.xlsx": "MHUK_MediaPlan_Master_NewBalance_Template_2023.xlsx"
        }
    }
}
```

## Update Schedule

The [Portal SharePoint Workflow](https://dbc-341b6afb-df67.cloud.databricks.com/jobs/1034177789938943?o=7058903129942627) runs daily at 12:00 PM.

## Manually Updating Files

To refresh files manually:

1. Click **Run Now** on the workflow.
2. Alternatively, run the [Main Notebook - Loop through all clients](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/3345174099368464?o=7058903129942627).

## Requesting a New SharePoint Client

Access to SharePoint depends on the `Sites` permissions assigned to the `Signal-Sharepoint` App. To enable access, request `site.selected` permissions for the relevant MediaPlan site.

### Request Process

Submit the request via email to **ESD@interpublic.com** with the following details:

- **App Name:** Signal-SharePoint
- **App ID URI:** api://9ce9a508-0766-4e8a-8a0d-74ce7ea74c25

