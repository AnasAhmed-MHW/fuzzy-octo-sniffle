---
title: Issues
parent: Brand Pulse
nav_order: 6
last_modified_date: 2025-01-23 12:00
---

# Issues


<br>Based on experience, most Brand Pulse issues fall into the following categories:

---

### 1. **Data Discrepancies: Missing Data**  
**Symptoms:**  
- Missing data for specific weeks.  

**Common Causes:**  
- **Raw Data Files Issues:**  
  - Entire weeks are missing from the files.  
  - The number of respondents in the file is incorrect.  
- **Data Join Issues:**  
  - Incorrect join between the date and data files.

**Solutions:**  
1. Contact Focal Data to request resending the waves with missing or incomplete data.  
2. Clearly specify the exact date and data files that are problematic.  
3. Once corrected files are available in the S3 bucket, rerun the workflow for those specific weeks.  

---

### 2. **Data Discrepancies: Incorrect Data**  
**Symptoms:**  
- Significant spikes or drops in results for specific weeks.  
- Missing responses for certain questions during a specific week.  
- Gaps in data that suggest incomplete or incorrect responses.  

**Common Causes:**  
- **Missing Responses:**  
  - Questions that allow multiple responses (e.g., select five options) may only capture partial responses in the dataset.  
- **Label Changes:**  
  - Slight modifications to question or response wording disrupt mapping.  
- **Data Duplication:**  
  - Duplicate rows in bronze, silver, or gold tables.

**Solutions:**  
1. **Check for Duplication:**  
   - Remove duplicated rows for `respondent x wave x question` combinations.  
   - Deleting multiple problematic waves and rerunning them often resolves the issue efficiently.  
2. **Request Missing Data:**  
   - If responses are incomplete, ask Focal Data to resend the raw data.  
3. **Update Mapping:**  
   - If questions or responses are relabeled, update the `mapping.py` file to reflect the changes and ensure proper alignment.  

---

### 3. **Workflow Failures**  
**Symptoms:**  
- Workflow fails to complete.  

**Common Causes:**  
- **Translation Module Failure:**  
  - Translation tasks do not execute fully.  
- **Conversion Issues:**  
  - Errors occur when converting from Spark to pandas.

**Solutions:**  
1. **Run Smaller Batches:**  
   - Process smaller timeframes (e.g., specific weeks) to isolate and address the issue.  
2. **Increase Cluster Size:**  
   - Allocate more resources to handle larger workloads and prevent memory-related failures.  

---

{: .important}  
> The Brand Pulse pipeline (for New Balance) is generally stable. 
> Most issues stem from changes in the raw data files.  
> 
> Always verify that the two raw CSV files (date and data) meet the expected format before troubleshooting further.
