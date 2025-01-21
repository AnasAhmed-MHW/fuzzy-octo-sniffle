---
title: Onboarding 
Parent: Adverity
nav_order: 2
last_modified_date: 2025-01-20 12:00
---

# Onboarding a New Client

## Workspaces  

To manage data effectively, navigate to the appropriate workspace from the [Datastreams page](https://mullenlowemediahub.datatap.adverity.com/datastreams/list/).  

You can see the available workspaces on the sidebar. 
When creating new workspaces, please ensure the *parent* Workspace is **Mediahub Global | Databricks**.
This will ensure authorisations and destinations can be shared between the child workspaces and the templates generated can be stored in the parent workspace **Mediahub Global | Databricks**.


### Additional Instances  
- **Value Retail Adverity**: This client uses a separate Adverity instance. Access it [here](https://valueretail.datatap.adverity.com/).  

---

## Guidelines for Workspaces  

#### 1. Handling New Clients or Expansions
When onboarding a new client or expanding services for an existing client:  
- **Create a New Workspace** to ensure clear separation between clients.  
- For **new clients**, set the **parent workspace** to `Mediahub Global | Databricks`

#### 2. Destinations and Authorisations
- When creating **new destinations** or **new authorisations**, configure them under the **Mediahub Global | Databricks** workspace.  
- This allows sharing across child workspaces.  
- If a client-specific configuration is required, use the client’s workspace instead.  


_Current State:_  
- The **Global Databricks workspace** contains multiple clients.  
- Value Retail uses its own Adverity instance which the client owns.  

---

## Creating a New Destination for a Workspace or Client  

When setting up new datastreams, ensure they are connected to S3 Buckets within AWS.  

### Steps to Create a New Destination  

#### 1. Ensure an S3 Bucket Exists  
Check if there is an appropriate S3 Bucket in the [AWS](https://d-9a673e003c.awsapps.com/start#/).  

#### 2. Create a New S3 Bucket (If Needed)  
If a new bucket is required:  
1. Select **Create Bucket**.  
2. Choose **General Purpose Bucket** type.  
3. Name the bucket in the following format:  
    ```
    mh-rawdata-clientname  
    ```  
    Example:  
    ```
    mh-rawdata-akzonobel
    ```  
4. Copy settings from an existing bucket, such as `mh-rawdata-valueretail`.  
5. Tick the box acknowledging that buckets and objects may be public.  
6. Update tags for `Client` and `Name` to reflect the client.  
7. Click **Create Bucket**.  

#### 3. Update Bucket Policy for Adverity Access  
The Adverity access to buckets is linked to the ARN:  
```
arn:aws:iam::251616991370:user/251616991370_MediaHub_S3Access_shared_user
```  
To provide access to the new bucket:  
1. Contact someone with `Admin` permissions in AWS or email `kimaya.joshi@interpublic.com`.  
2. Request an update to the bucket policy to include the new bucket.  

#### 4. Create a New Destination in Adverity  
1. Navigate to **Destinations** in Adverity and create a new destination.  
2. Select **File** as the destination type.  
3. Use the `New S3 | All Clients` Authorisation Option.  

#### 5. Configure Destination Options  
1. Name the destination using the format:  
    ```
    S3 | MHxClientName
    ```  
    Example:  
    ```
    S3 | MHxAkzoNobel
    ```  
2. Set the destination URL as:  
    ```
    s3://eu-west-1.amazonaws.com/{bucket-name}
    ```  
3. Configure the following settings:  
   - **File Format** > Output Format: **CSV (with semicolon)**  
   - **Data Mapping** > Data Mapping: **Enabled (with metadata)**  
   - **Data Mapping** > New Line Mode: **Surround string with quotation mark**  

#### 6. Standardise Folder Structure in Databricks  
Use the [S3 Folder Creation Notebook](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/1126773199173661?o=7058903129942627#command/1126773199173662) in Databricks to create a standardised folder structure in the new bucket.  

_Use the notebook's output to inform your destination file name template._  

---