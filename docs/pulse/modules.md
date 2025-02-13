---
title: Modules + Gold Tables
parent: Brand Pulse
nav_order: 5
last_modified_date: 2025-01-23 12:00
---

# New Balance Survey Pipeline

The New Balance survey data pipeline is structured into multiple tables, each serving a distinct analytical purpose. However, performance issues—particularly **Spark pivot operations taking excessive time**—have been observed. These delays appear to be caused by **garbage collection and inefficient partitioning strategies**.  

### **Potential Performance Optimisation**  
- Investigate **partitioning strategies** to improve efficiency.  
- Test different configurations to determine if the entire transformation process can remain within Spark.  
- Monitor **garbage collection** to identify bottlenecks.  

---

## **Pipeline Overview**  

### **1. Meta Table**  
The **Meta table** categorises respondents based on demographics and audience segmentation.  

- Unique on: `respondent_id` and `wave`.  
- Processes:  
  - Filters relevant **categorisation questions**.  
  - **Pivots responses** for structured storage.  
  - Defines **audiences** based on criteria provided by Anthony.  

📌 **Key Challenge:** **Pivoting** operations within Spark can be slow, requiring partitioning optimisations.  

---

### **2. Funnel Table**  
Captures the **brand funnel stages** (awareness, consideration, purchase, etc.) across all brands.  

- Unique on: `respondent_id`, `wave`, and `brand`.  
- Additional column: **Competitor brands & benchmarks**.  

#### **Processing Steps**  
1. **Filter & Pivot Brand Funnel Questions**  
   - Includes **cultural relevance scoring** mapped to a ± system.  
   
2. **Process Advocacy Question (Favourite Brand)**  
   - Handled separately as it contains **free-text responses**.  

3. **Spontaneous Awareness & Ad Awareness Handling**  
   - **Text-to-brand mapping** ensures consistency and corrects misspellings.  
   - Uses the `texttobrands` table for efficient translation and fuzzy matching.  
   - **New brands and misspelled entries** are automatically appended for future reference.  

| Raw Response | Translated Response | Mentioned Brands |
|-------------|---------------------|------------------|
| new balance、nike、adidas、converse、puma、オニツカタイガー、reebok、asics | New Balance, Nike, Adidas, Converse, Puma, Onitsuka Tiger, Reebok, Asics | ["New Balance", "Nike", "Adidas", "Converse", "Puma", "Reebok", "Asics"] |

4. **Generate Mention Order Tables**  
   - Determines **1st, 2nd, and 3rd** brand mentions.  
   - Identifies whether a brand was **mentioned at all**.  

5. **Join All Processed Data to Form the Final Funnel Table**  

📌 **Key Challenge:** **Text-to-brand matching** must be optimised to reduce computation time while maintaining accuracy.  

---

### **3. Audience Table**  
Designed for **Power BI visualisations** by restructuring audience data.  

- **Transforms audience data from the Meta table**.  
- Assigns `1` to each audience category for easier aggregation.  
- **Melts the data** so that each row contains only `respondent_id` and `audience_type`.  

📌 **Key Benefit:** **Simplifies audience-based reporting** in Power BI.  

---

### **4. Celebrity Table**  
Functions similarly to the Funnel table, but its unique values are:  
- `respondent_id`, `wave`, and `celebrity`.  

📌 **Key Feature:** **Tracks brand association with celebrities** using a structured format.  

---

### **5. Multi-Answer Table**  
Stores survey responses in **long format** rather than pivoting.  

- **Filters and categorises relevant questions**.  
- Cleans data for **visualisation compatibility**.  
- Joins with **market data** to correctly categorise sports (e.g., distinguishing "Football" from "American Football").  

📌 **Key Difference:** Unlike other tables, this does **not** pivot responses.  

---

### **6. Brand Association Table**  
Handles **matrix-style questions**, where respondents associate brands with attributes or taglines.  

#### **Example Question Format:**  
```  
"Which ONE, if any, of the following brands do you think has the following tagline? | Nike | We Got Now"  
```  
- **Multiple options per respondent** require careful structuring.  
- **Standardisation functions** ensure consistency across different survey iterations.  
- Final structure mirrors the **Funnel table** format.  

📌 **Key Challenge:** **Frequent question format changes require adaptive transformations**.  

---

## **Final Thoughts**  
This pipeline is a little messy but is stable for New Balance

### **Next Steps for Improvement:**  
- [ ] **Investigate Spark partitioning** to reduce pivot execution times.  
- [ ] **Optimise text-to-brand matching** to minimise processing overhead.  
- [ ] **Monitor garbage collection** for potential memory management improvements.  
