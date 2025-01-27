---
title: AWS Bucket
parent: RADAR
nav_order: 5
last_modified_date: 2025-01-20 12:00
---

# S3 Bucket

The `mh-mediaplans` S3 Bucket is designed to store and manage MediaPlans. Each client has a dedicated folder, which aligns with their corresponding database name in Databricks. Within each client folder, there are four subfolders:

- **uploads**
- **success**
- **failure**
- **archive**

{: .warning}
> When onboarding a new client ensure the client folder name matches the databricks schema name. 
> Ensure there are the four above folders

## How the MediaPlan S3 Bucket Works

1. **Uploading MediaPlans**:
   - When a MediaPlan is uploaded in RADAR, it is initially placed in the `uploads` folder.

2. **Categorisation**:
   - The tool processes the uploaded MediaPlan and categorizes it based on its status:
     - Successful plans are moved to the `success` folder.
     - Failed plans are moved to the `failure` folder.

3. **Handling Duplicates**:
   - If a MediaPlan with the same ID or filename already exists in the `success` or `failure` folder:
     - The older file is moved to the `archive` folder.
     - The latest file remains in the `success` or `failure` folder, ensuring no duplicates exist in these folders.

## Key Rules
- Each client folder must contain the `uploads`, `success`, `failure`, and `archive` subfolders.
- No duplicate MediaPlans (based on ID or filename) should exist in the `success` or `failure` folders.
- Archived files serve as a history of older versions of the same MediaPlan.

{: .warning}
> Should there be a loading issue with the RADAR app on the portal this may be due to the number of files that can be loaded by the client-portal API app.
> Consider moving _archived_ files into a parent **{client}_archive** folder. 