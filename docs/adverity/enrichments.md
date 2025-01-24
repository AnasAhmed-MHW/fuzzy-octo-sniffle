---
title: Enrichments  
parent: Adverity  
nav_order: 7  
last_modified_date: 2025-01-23 12:00  
---

# Enrichments  

Enrichments in Adverity allow you to transform and standardise your data before it’s sent to a destination. 

---

## Enrichment Aim  

Alvi's aim with Enrichments in Adverity is to help gather more information within the raw table or to simplify and improve the compute effiecencies within Databricks without losing transparency in the transformation steps

---

## How to Create and Apply Enrichments  

### 1. **Navigate to Transformations**  
- Go to **Manage Data** > **Transformations** in the Adverity dashboard.  
- Click on **Create Transformation** to start building a new enrichment.  

---

### 2. **Choose the Right Transformation Type**  
- **Custom Script**:  
   - Select this option for maximum flexibility, allowing you to define specific rules and logic for your enrichment.  

---

### 3. **Workspace Selection**  
- Set the workspace to `MediaHub Global | Databricks`  
   - This ensures that the enrichment is available across child workspaces and can be shared among different teams or clients.  

---

### 4. **Creating the Transformation Logic**  

#### **ExtendMissing**  
- Add all expected field names to ensure that missing columns are automatically filled.  
- Use the **Source** button in Adverity to quickly pull in the required fields for your datastream type.  

#### **Reorder**  
- Arrange the field names in a logical order for readability:  
   - **Dimensions first** (e.g., Campaign Name, Ad Group, Date).  
   - **Metrics second** (e.g., Clicks, Impressions, Spend).  
- Reordering helps maintain a clear and consistent data structure across all datastreams.  

---

### 5. **Placement of Enrichments**  
- Place this transformation **before the Meta Column Addition Enrichment** in your data pipeline.  
   - This ensures the data structure is finalised before additional metadata is appended.  

---

## Additional Best Practices  

### **Using Templates for Efficiency**  
- Save frequently used enrichments as templates.  
- Templates can be shared across workspaces, ensuring consistency and reducing setup time.  

### **Testing Your Enrichment**  
- After creating an enrichment, run a sample dataset to verify:  
   - Column order and structure.  
   - Any missing or incorrectly mapped fields.  

### **Documentation**  
- Document each enrichment with a clear description of its purpose and logic.  
- This helps teams understand the transformations and reduces onboarding time for new users.  

---

## Example Enrichments  

### **ExtendMissing + Reorder**  
- Ensures a consistent column structure by filling in missing fields and arranging them in the desired order.  
- This is particularly critical when working with multiple files over time. For example:  
   - On **Day 1**, column 3 might represent the **Date**.  
   - On **Day 231**, column 3 might unexpectedly represent a **Metric**.  
  
  {: .important}
  Using this enrichment ensures the column order remains consistent across all files, eliminating confusion and preventing downstream processing errors.  

---

### **Meta Column Addition**  
- Appends standardised metadata fields (e.g., **Campaign ID**, **Ad ID**) to maintain uniformity across datasets.  
- This enrichment ensures that essential identifiers are always present, aiding in data aggregation and analysis.  
- Example configuration:  
   ```
   All \ Add Meta Col | Canonical Meta Col Add  
   ```  

---

### **Dates, IDs, and Currency Considerations**  
- Depending on the datastream, it is often more efficient and accurate to format raw data directly at the source. Examples include:  
   - **Dates**: If the raw data contains inconsistent formats (e.g., `Fri, 10 Jun 2023`), transform it into a standard date format (`YYYY-MM-DD`) at the source or through an enrichment.  
   - **IDs**: Missing columns or identifiers (e.g., Campaign IDs) should be added at the source where possible to ensure clean and complete datasets.  
   - **Currency**: Ensure that monetary values are formatted consistently (e.g., use the same decimal separator, currency symbol, or ISO code).  

{: .note}
Use your judgment to decide when a transformation is better applied at the source or within Adverity. Prioritise transparency, accuracy and simplicity, and always document changes clearly for future reference. AND Try keep things consistent.


