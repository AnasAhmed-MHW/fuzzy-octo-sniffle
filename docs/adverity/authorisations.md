---
title: Authorisations 
parent: Adverity
nav_order: 4
last_modified_date: 2025-01-20 12:00
---

# Managing Authorisations

## Creating a New Authorisation for a Platform  

When creating a new Datastream or Pipeline, you need to ensure you have the necessary access.  
For ease, we funnel all access to `adtech.analytics@mediahubww.com` to avoid issues in case someone leaves or for managing access across multiple email users.

### Steps to Create an Authorisation:  

1. Request an Admin of the platform to grant access to `adtech.analytics@mediahubww.com`.  
2. Go to the [Authorisations page](https://mullenlowemediahub.datatap.adverity.com/workspaces/4485e444-2c19-4b0c-ab86-bab95e887181/authorizations/) in Adverity and click **Create Authorisation**.  
3. Search for the name of the authorisation you wish to create.  
4. Click **Authorise Using Your Credentials**.  
5. Name the authorisation according to the following naming convention:  

    ```
    ACCOUNT_USED_FOR_ACCESS | PLATFORM_NAME | ACCOUNTS_GIVEN_ACCESS_TO
    ```  

    Example:  
    ```
    AdTech | Google Ads | All Accounts
    ```  

{: .note}
You can also choose to **Authorise Using Someone Else's Credentials**. This option will send an email to the user in question and prompt them to share access to Adverity.  

**Downsides of This Approach** 
This may result in duplication of Datastreams, as a single Datastream can only use one authorisation.  

---

## Datastream Setup  

### General Considerations  

- **Consistency**: Ensure datastreams are consistent across clients to maintain uniform pipelines.  
- **Templates**: Use or create templates for each datastream platform type to streamline the process.  
- **Granularity**: Build datastreams as granular as possible. Include IDs alongside dimension names (e.g., Campaign ID and Campaign Name). We should in almost all cases have a daily breakdown.
- **Enrichments**: Use enrichments like `Extend + Reorder` to ensure consistent column structures and data integrity.  


### Creating and Using Datastream Templates  

- **Creating Templates**:  
  1. Open an existing datastream.  
  2. Under **More**, click **Save as Template**.  
  3. Name the template with the prefix **SIGNAL** for easy identification.  


### Creating a New Datastream (Without a Template)  

1. **Create Datastream**:  
   - Click **Create Datastream** and search for the platform type.  

2. **Select Authorisation**:  
   - Choose an existing authorisation or create a new one. Refer to [Creating a New Authorisation for a Platform](#creating-a-new-authorisation-for-a-platform) if needed.  

3. **Filter Client Accounts**:  
   - If the authorisation covers multiple accounts, filter to the specific client accounts.  

4. **Select Metrics and Fields**:  
   - Choose granular metrics and fields. Include all relevant data to minimize change requests later.  

5. **Connect to Destination**:  
   - Link the datastream to the appropriate destination. Refer to the [Destination Section](#destination-section) for instructions.  

6. **Initial Fetch**:  
   - Run an initial data fetch to verify the setup.  

7. **Add Extend + Reorder Enrichment**:  
   - Use the `ExtendMissing + Reorder` enrichment for consistent column order.  
   - If no enrichment exists for this datastream type, create one following the [Enrichments Section](#enrichments).  

8. **Add Meta Column Enrichment**:  
   - Include the existing enrichment:  
     ```
     All \ Add Meta Col | Canonical Meta Col Add
     ```  

9. **Set Scheduling**:  
   - Fetch a last X number of days - this number should be governed by the data freshness of the platform or the conversion lookback window.
   - Naming convention datastreams: Fetch **365 days** for historical data.  

10. **Data Mapping**:  
    - Configure data mapping for the datastream. Refer to the [Data Mapping Section](#data-mapping-section).  

11. **Name the Datastream**:  
    - Follow this naming convention:  
      ```
      CLIENT_NAME | PLATFORM | GRANULARITY | DATASTREAM_TYPE
      ```  
      Example:  
      ```
      New Balance | DoubleVerify | Ad | Media Delivery
      ```  

---

