---
title: Akzonobel
layout: default
nav_order: 10
last_modified_date: 2025-01-20 12:00
---
# AkzoNobel

## Rough SQL Overview

### Database Details
Stored in the MySQL Database:
- **Hostname**: `mlmdata-analytics-cluster.cluster-czxtihb3zgvk.eu-west-1.rds.amazonaws.com`  
- **Username**: `mh.data`  
- **Password**: Contact the Engineering Team.  
- **Client/Database**: `client_akzonobel`

### Table Naming Conventions
Tables follow a structured naming convention:

1. **`av_`** – Raw tables from Adverity
2. **`pr_`** – Media delivery data only (impressions, clicks, spend)
3. **`cv_`** – Conversion data only
4. **`ex_`** – External datasets (likely manually added)
5. **`parsed_`** – Naming convention table delimited
6. **`kpi`** – Contains both media delivery and conversions
7. **`mp`** – Mapping tables (e.g., for geographic data)
8. **`prod`** – Tables ready for dashboarding

Additionally:
- A number suffix (e.g., `pr_1`) indicates its order in the stored procedure pipeline.
- Stored Procedures (SPs) are named similarly to the corresponding table but with an `sp_` prefix. Example:
  ```
  Table:            prod_3_googleads_ad
  Stored Procedure: sp_prod_3_googleads_ad
  ```

## Useful SQL Snippets

To find scheduled procedures:
```sql
SELECT * FROM information_schema.events;
```

To check currently running processes:
```sql
SHOW PROCESSLIST;
```

## Naming Convention Tables
The stored procedure `sp_signal_name_update` is responsible for identifying different channels and extracting unique platform values. These values are then categorized into three tables (Search, Social, Display) before further processing in Databricks.

## Updating SQL Stored Procedures
### Important Warnings:
- **Always take a backup** before modifying any stored procedures.
- **Never directly overwrite** an existing stored procedure without verifying the changes.
- **Ensure proper testing** in a non-production environment before deploying changes.

### Steps for Updating a Stored Procedure
1. **Backup the Current Stored Procedure**  
   Retrieve and save the existing SP definition:
   ```sql
   SHOW CREATE PROCEDURE sp_your_procedure_name;
   ```
   
2. **Rename the Existing Stored Procedure (for rollback safety)**  
   This helps in quickly reverting in case of errors:
   ```sql
   RENAME PROCEDURE sp_your_procedure_name TO sp_your_procedure_name_backup;
   ```
   
3. **Delete the Current Stored Procedure**  
   If renaming is not feasible, delete the procedure before creating a new one:
   ```sql
   DROP PROCEDURE IF EXISTS sp_your_procedure_name;
   ```
   
4. **Create the New Stored Procedure**  
   Run the updated stored procedure script:
   ```sql
   DELIMITER ;; # make sure you redefine a delimiter
   # the definer should be your user name and after procedure is the name of the procedure
   CREATE DEFINER=`root`@`%` PROCEDURE `sp_abc`() 
   BEGIN

   # Here is where your SQL statment will live
    
   END;;
   DELIMITER ; # return the delimter back to what was previously done
   ```
   
5. **Validate the Changes**  
   Ensure the procedure has been created successfully:
   ```sql
   SHOW PROCEDURE STATUS WHERE Name = 'sp_your_procedure_name';
   ```
   
6. **Run a Test Execution**  
   ```sql
   CALL sp_your_procedure_name();
   ```
   Check the logs and results for any unexpected errors.
   
7. **Remove the Backup (if all tests pass)**  
   ```sql
   DROP PROCEDURE IF EXISTS sp_your_procedure_name_backup;
   ```

