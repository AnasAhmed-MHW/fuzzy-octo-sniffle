---
title: Datastreams
parent: Adverity
nav_order: 5
last_modified_date: 2025-01-23 12:00
---

# Datastream Setup  

Setting up datastreams correctly ensures consistent, reliable data pipelines. Here's everything you need to know:  

---

## Key Guidelines  

- **Stay Consistent**: Keep datastream setups uniform across clients to streamline maintenance.  
- **Use Templates**: Save time by creating or using pre-existing datastream templates for each platform type.  
- **Get Granular**: Always aim for the most detailed level of data, such as including **IDs** (e.g., Campaign ID) alongside names. A daily breakdown is recommended for almost all cases.  
- **Leverage Enrichments**: Use enrichments like `Extend + Reorder` to maintain consistent column structures and data accuracy.  

---

## Naming your datastream  

Follow this naming format for datastreams:  
```
CLIENT_NAME | PLATFORM | GRANULARITY | DATASTREAM_TYPE
```  
```
Example:
New Balance | DoubleVerify | Ad | Media Delivery
```  

---

## How to Use Datastream Templates  

To simplify your workflow, leverage existing Datastream templates. These templates are typically saved under the prefix `SIGNAL`. <br>Alternatively, you can use a Datastream from another client as a reference—convert it into a template and use it to guide the creation of new Datastreams.

### Create a New Template  
1. Open an existing datastream.  
2. Click **More** > **Save as Template**.  
3. Name the template with the prefix **SIGNAL** for easy identification.  

---

## Creating a Datastream from Scratch  

### 1. Create the Datastream  
- Click **Create Datastream** and search for the relevant platform type.  

### 2. Select Authorisation  
- Choose an existing authorisation or create a new one.  
- If needed, check the guide on [Creating a New Authorisation for a Platform](#creating-a-new-authorisation-for-a-platform).  

### 3. Filter Client Accounts  
- If the authorisation supports multiple accounts, filter down to the specific client account.  

### 4. Choose Metrics and Fields  
- Select detailed metrics and fields to cover all reporting needs upfront and avoid later changes.  

### 5. Connect to a Destination  
- Link the datastream to the correct destination. Refer to the [Destination Section](#destination-section) for instructions.  

### 6. Run Initial Fetch  
- Perform an initial data fetch to verify everything is set up correctly.  

---

## Enrichment Setup  

Enrichments are essential for simplifying transformations in Databricks and ensuring data is consistent and easy to work with.

While it’s possible to heavily rely on Adverity enrichments, I (Alvi) personally prefer to use only the minimal necessary enrichments. This approach promotes full transparency in the Databricks workflow. However, there are trade-offs to consider—balancing transparency in the code with the time required to set up the process is key.

Here are the two enrichments I frequently use:

### 1. **Extend + Reorder**  
- Apply the `ExtendMissing + Reorder` enrichment to maintain consistent column ordering.  
- If one doesn't exist for the datastream type, create it by following the [Enrichments Section](#enrichments).  

### 2. **Meta Column Enrichment**  
- Include this enrichment for canonical meta columns:  
   ```
   All \ Add Meta Col | Canonical Meta Col Add  
   ```  

---

## Scheduling and Fetching  

### Scheduling Rules  
- Fetch data for the **last X days** (based on platform data freshness or the conversion lookback window).  

### Historical Fetch  
- For historical data, fetch **365 days** to ensure full coverage.  
  
---

## Quick Tips  

- **Templates Save Time**: Always check for reusable templates before starting from scratch.  
- **Be Granular**: Include all relevant IDs and breakdowns from the start to minimize back-and-forth adjustments.  
- **Verify with Fetch**: Running an initial fetch ensures your datastream is working correctly.  
- **Use Raw Fetch**: When QA'ing it is best to use the 'Fetch Raw Data' option to ensure no enrichments or transformations by Adverity is the root cause. It will also let you download the data without it being inputted into the destinatiopn.
