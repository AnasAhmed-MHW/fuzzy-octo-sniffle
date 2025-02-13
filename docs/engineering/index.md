---
title: Engineering Standards
layout: default
nav_order: 6
last_modified_date: 2025-01-20 12:00
---


# Alvi's Dream

The vision is simple: **a pipeline that is accurate, reliable, and scalable**—so robust that debugging is effortless, and onboarding new clients is a breeze. The key to achieving this lies in **standardisation, logging, and rigorous testing**.  

## **Core Principles**  

### 1. **Standardise Everything**  
Consistency is the foundation of a scalable system. Define clear standards for:  
- **Data schemas** – Ensure uniform data structures to prevent inconsistencies.  
- **Adverity data stream settings** – Maintain a standardised configuration for smooth integration.  
- **Client-Specific Processes** – When unique client needs arise, consider how they might apply across multiple clients. Strive for reusable, standardised solutions instead of ad hoc fixes.  

### 2. **Ensure Accuracy & Completeness**  
Accurate and complete data flow is critical to performance. To achieve this:  
- **Verify access** – Confirm that all **advertisers, accounts, and campaigns** are included in the data feeds.  
- **Understand platform structures** – Platforms may separate activities across accounts (e.g., **Search ads vs. YouTube ads**). Map out these structures to avoid gaps in reporting.  
- **Monitor data freshness** – Understand the **refresh windows** of different platforms to ensure that Adverity picks up data at the right intervals.  

### 3. **Test Rigorously**  
Every process should be validated through **automated and manual testing**:  
- **Post-process validation** – Ensure joins between datasets are correct.  
- **Data type verification** – Confirm that data types match expected formats to prevent processing errors.  
- **Automated data quality checks** – Implement tools like **DQX** and **Great Expectations** to verify:  
  - Data completeness and consistency.  
  - Schema adherence and format validation.  
  - Freshness of data across different sources.  

By embedding these principles into the pipeline’s design, we create a system that is **scalable, maintainable, and resilient**, ensuring high-quality data and seamless client onboarding.  


## Things to do in 2025

1. Migrate to Metastores!
2. Shift all ETL Notebooks to datastream-etl!
3. Adding Tests post workflow
4. Standardise logging!
5. Easy Manual Overrides!
6. Standardise the Forecasting Tables

