---
title: Onboarding - Destinations
parent: Adverity
nav_order: 3
last_modified_date: 2025-01-23 12:00
---

# Destinations in Adverity  
Where your data gets sent  

## Setting Up a New Destination for a Workspace or Client  

When creating new datastreams for a client, you’ll usually need to connect them to an **S3 Bucket** in AWS. Let’s walk through the process step by step:  

---

## 1. Check for an Existing S3 Bucket  

Before creating anything new, confirm if there’s already an appropriate S3 Bucket in AWS.  
- Log in to [AWS](https://d-9a673e003c.awsapps.com/start#/).  
- Look for an S3 Bucket that matches the client.  

---

## 2. Create an S3 Bucket (If Needed)  

If no suitable bucket exists:  

1. Go to **S3** in AWS and click **Create Bucket**.  
2. Select **General Purpose Bucket**.  
3. Name the bucket using this format:  
    ```
    mh-rawdata-clientname  
    ```  
    
    ```
    Example
    mh-rawdata-akzonobel  
    ```  

4. Copy settings from an existing bucket (e.g., `mh-rawdata-valueretail`).  
5. Acknowledge the checkbox for public access to buckets/objects.  
6. Add tags to reflect the **Client** and **Name**.  
7. Click **Create Bucket**.  

---

## 3. Grant Adverity Access  

Adverity needs access to the S3 bucket via the following ARN:  
```
arn:aws:iam::251616991370:user/251616991370_MediaHub_S3Access_shared_user  
```  

To update permissions:  
1. Contact an AWS Admin (currently _Harrison_) or email `kimaya.joshi@interpublic.com`.  
2. Request the bucket policy be updated to include the new bucket.  

---

## 4. Create a Destination in Adverity  

Now, configure the destination in Adverity:  
1. Go to the **Destinations** section in Adverity.  
2. Click to create a new destination.  
3. Choose **File** as the destination type.  
4. Use the `New S3 | All Clients` authorisation option (This will contain the current Access key and Secret ID for the Adverity IAM)

---

## 5. Configure the Destination  

1. Name the destination following this format:  
    ```
    S3 | MHxClientName  
    ```  
    ```
    Example
    S3 | MHxAkzoNobel  
    ```  
2. Set the destination URL as:  
    ```
    s3://eu-west-1.amazonaws.com/{bucket-name}  
    ```  
3. Adjust these settings:  
   - **File Format**: Set Output Format to **CSV (with semicolon)**.  
   - **Data Mapping**: Enable Data Mapping with metadata.  
   - **New Line Mode**: Surround strings with quotation marks.  

---

## 6. Standardise Folder Structure  

For a clean setup, create a standardised folder structure in the S3 bucket:  
1. Open the [S3 Folder Creation Notebook](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/1126773199173661?o=7058903129942627#command/1126773199173662) in Databricks.  
2. Run the notebook to generate the folder structure.  

{: .important}  
Use the output from the notebook to set up your destination’s file name template.  
