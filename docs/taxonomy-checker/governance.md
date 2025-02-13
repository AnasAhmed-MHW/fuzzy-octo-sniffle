---
title: Taxonomy Governance
parent: Taxonomy Checker
nav_order: 1
last_modified_date: 2025-02-03 12:00
---

# Taxonomy Governance  

This guide outlines the configuration requirements for the Taxonomy Checker, found in the `Meta` tab of the governance document. The `Meta` tab consolidates different configurations of Taxonomy Versions, ensuring consistency and accuracy across taxonomies.  

---  

## Key Headers and Their Purpose  

Each header in the `Meta` tab serves a specific purpose, defining how taxonomies are validated and managed within the Taxonomy Checker.  

- **`Format`**  
  Defines the expected naming convention of the taxonomy.  
  - Aligns with headers in the `Shared Values` tab.  
  - Use `Freeform` to bypass checks.  
  - Multiple values should be separated by commas `,`.  

- **`Table`**  
  A legacy column referencing the SQL table to be checked. Retained for backward compatibility but not actively used.  

- **`Channel`**  
  Categorizes the taxonomy (e.g., Search, Social, Display, YouTube). Ensures taxonomy formats are matched against their respective categories.  

- **`Channel Alias`**  
  Represents a granularity level (e.g., `Search Campaign`). Clarifies which format is being validated against the taxonomy name.  

- **`Column to validate`**  
  Specifies the column from the dataset being checked. Ensures the correct data is validated against the taxonomy rules.  

- **`Freeform`**  
  Values here, if matched with the `Format`, are ignored during validation, treating them as freeform fields.  

- **`Breadcrumbs`**  
  Provides a hierarchical path for context, typically including identifiers like `advertiser_id`, `advertiser_name`, and `campaign_id`. Helps trace taxonomy origins.  

- **`Delimiter`**  
  Specifies the character used to separate values within a field, commonly `_`.  

- **`Date field`**  
  A legacy column for fetching the date from the SQL table. Retained for backward compatibility, not actively used.  

- **`Taxonomy version`**  
  Indicates the version of the taxonomy (e.g., `TX1`), ensuring the correct rules and configurations apply.  

- **`TV Start Date` & `TV End Date`**  
  Define the validity period of the taxonomy version. Taxonomies are valid only if the current date falls within this range.  

- **`Allow Optional Ending`**  
  A boolean flag (`TRUE` or `FALSE`) indicating if an optional ending is allowed in the taxonomy name. Enforces strict adherence to the specified format when `FALSE`.  

- **`Length`**  
  Reflects the length of the inputted format, serving as a visual QA tool to confirm the format's correctness. This does not account for the `Allow Optional Ending`.  

---

### Example Configuration  

Here’s an example row from the `Meta` tab to illustrate a typical configuration:  

| Format                                                                 | Table | Channel | Channel Alias     | Column to validate | Freeform | Breadcrumbs                          | Delimiter | Date field | Taxonomy version | TV Start Date | TV End Date | Allow Optional Ending | Length |
|------------------------------------------------------------------------|-------|---------|-------------------|--------------------|----------|--------------------------------------|-----------|------------|------------------|---------------|-------------|-----------------------|--------|
| Taxonomy Version,Village,Channel,Country,Audience Type,Location,Language,Keyword Type,Keyword Match Type,Targeting freeform,Funnel,Optimisation KPI,Experiment,freeform |       | search  | Search Campaign   | campaign_name      | Targeting freeform, freeform | advertiser_id, advertiser_name, campaign_id | _         | end_date   | TX1              | 2023-05-01    | 2024-03-31  | FALSE                 | 14     |

---

### Additional Headers (Proposed)  

To enhance the functionality of the Taxonomy Checker, consider adding:  

- **`Validation Rules`**  
  Defines specific rules or regex patterns for validating the taxonomy format (e.g., ensuring fields contain only alphanumeric characters).  

- **`Required Fields`**  
  Lists fields that must be populated for a valid taxonomy, ensuring no critical information is missing.  

