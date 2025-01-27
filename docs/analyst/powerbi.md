---
title: PowerBI
parent: Analyst Engineering Guide
nav_oder: 4
last_modified_date: 2025-01-23 12:00
---

# PowerBI

## Connecting Databricks to Power BI

To establish a connection between Power BI and Databricks, follow these steps:

#### Within Databricks:
1. Log into Databricks: [Databricks Login](https://dbc-341b6afb-df67.cloud.databricks.com/).  
2. Click your account name in the top-right corner and go to **Settings**.  
3. Under the **User** subheader, select **Developer**.  
4. In the **Access Tokens** section, click **Manage**.  
5. Generate a new token and optionally provide a description.  
6. **Important**: Copy the token immediately and store it securely, as it will not be displayed again.

#### Within Power BI:
1. Click **Get Data** or navigate to **File > Get Data**.  
2. Search for **Databricks** and select the **Azure Databricks** connector.  
3. Click **Connect**.  
4. Enter the required details for the compute cluster being used:  
   - **Host**: `dbc-341b6afb-df67.cloud.databricks.com`  
   - **HTTP Path**: `sql/protocolv1/o/7058903129942627/0209-113722-jcsrnoj7`  
   *(As of January 2025, the default cluster is the **DataOps Shared Compute Cluster**.)*  
5. Choose a **Data Connectivity mode**:  
   - **Direct**: Enables live refreshes.  
   - **Import**: Requires scheduled refreshes.  
6. Click **OK**.  
7. For the **Authentication Method**, select **Personal Access Token** and enter the token you generated in Databricks.  
8. Click **Connect** to establish the connection.

---

## Power BI Embedded Issues: Common Root Causes and Resolutions  

In my experience, nearly all Power BI Embedded issues can be traced back to four key areas: **Credential Issues**, **Memory Issues**, **Initial Configuration Issues** and **Schema Changes**. <br>Here's a deeper dive into each category and practical steps to address them.  

### 1. **Credential Issues**  
   **Symptoms:**  
   - Dashboards or reports fail to load.  
   - Authentication errors or timeout messages.  
   - Users see "Access Denied" or "Unauthorised" messages.  

   **Common Causes:**  
   - Incorrect or expired tokens.  
   - Improper OAuth configuration.  
   - Lack of appropriate permissions for users or applications.  

   **Solutions:**  
   - Ensure you are using the correct token and connection type. 
   - If you have an expiry date - regularly rotate and refresh your secrets to avoid expiration issues.  

---

### 2. **Memory Issues**  
   **Symptoms:**  
   - Reports are slow to load or fail to render completely.  
   - Reports do not load on the website but load within PowerBI
   - Server-side errors related to insufficient memory or resource constraints.  
   - Poor performance when interacting with large datasets.  

   **Common Causes:**  
   - Insufficient resource allocation on the capacity tier (e.g., **A1**, **A2**, or **P1**).  
   - Complex reports with heavy visuals, filters, or inefficient data models.  
   - Memory leaks due to poorly optimised custom visuals or embedding code.  

   **Solutions:**  
   - Remove unecessary Reports
   - Optimise your reports by:  
     - Reducing the number of visuals on a page.  
     - Using aggregated or summaris  ed data models instead of raw datasets.  
     - Removing unused columns and relationships from the dataset.  
   - Scale up your capacity in Azure to meet the needs of your report workloads. For example, move from **A1** to **A3** or **P1** if usage consistently exceeds limits.  

   **Best Practices:**  
   - Use dedicated capacities for large-scale solutions to avoid performance degradation due to multi-tenant usage.  
   - Regularly monitor memory and CPU usage using Azure Monitor or Power BI Embedded metrics.  

---

### 3. **Initial Configuration Issues**  
   **Symptoms:**  
   - Reports don’t display after embedding.  
   - Errors during embedding setup, such as "Unable to find the dataset" or "Report not found."  
   - Embedded functionality works in development but not in production.  
   - Tables do not appear within PowerBI

   **Common Causes:**  
   - Incorrect workspace or HTTP used in the embedding process.  
   - Misaligned configurations between Power BI Service, Azure, and the embedding application.  

   **Solutions:**  
   - Double-check the workspace, dataset, and report IDs in your code to ensure they align with what’s published in the Power BI Service.  
   - Confirm that you are using the correct cluster path and url.   

---

### 4. **Schema Change Issues**  
   **Symptoms:**  
   - Refresh errors occur.  
   - "Data Source Error" messages are displayed.  
   - Visuals fail to render or display incorrect data.  

   **Common Causes:**  
   - Changes to the table structure, such as renamed columns or altered data types.  
   - Mismatched data types in the source data compared to the Power BI model.  

   **Solutions:**  
   - Ensure all column names and data types in the source data match the Power BI model.  
   - If schema changes occur, update the Power BI model to reflect the new structure.  
   - Perform a full refresh of the dataset after making any schema adjustments.  
   - Use Power Query to validate and transform data types as needed to maintain consistency.  
