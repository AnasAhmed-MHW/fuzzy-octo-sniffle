---
title: MediaPlan Governance
parent: RADAR
nav_order: 4
last_modified_date: 2025-01-27 12:00
---

# MediaPlan Governance

This guide outlines the configuration requirements for the MediaPlan Template, located in the `MediaPlan` tab of the governance document.

All these configurations are extracted and defined as values in the `MediaPlanVars` class. 

---

## Key Headers and Their Purpose

### General Information

- **`Version`**  
  Indicates the version of the MediaPlan being used for the configurations.  
  - A row labeled `SCHEMA` is mandatory. This row defines the base schema for the bronze table and must include the following columns:  
    - `BaseMandatoryColumns`  
    - `BaseOptionalColumns`  
    - `MetaKeys`  
    - `AdditionalDateCols`

---

### File Details

- **`Filename Format`**  
  Specifies the expected naming convention for files. These names must align with the `Shared Values` headers.  
  - Use `Freeform` to bypass delimiter checks.  
  - Delimit terms in the filename with a separator defined in `Filename delimiter`.

- **`Filename delimiter`**  
  Defines the delimiter used in filenames, typically `_`.

---

### MediaPlan Template Tabs

- **`Tabs`**  
  Lists the required tabs in the MediaPlan Excel template.  
  - Case- and space-sensitive.  
  - Delimited by commas.

- **`SkipRows`**  
  Specifies the number of rows to skip in the main MediaPlan table where planning information resides.

- **`Meta SkipRows`**  
  Specifies the number of rows to skip in the meta table, usually located in the top-right corner of the tab. This table contains consistent information for all line items within the tab.

- **`HeaderSpan`**  
  Defines the row positions to convert into a MultiIndex header.  

  **Example Usage (Python):**  
  ```python
  df = pd.read_excel(
      io=path,
      sheet_name=sheet,  # Matches a tab name from `Tabs`
      skiprows=skip_rows,  # Number of rows to skip (SkipRows)
      header=header_span,  # HeaderSpan row positions
      keep_default_na=False,
  )
  ```

---

### Weekly Flighting and Columns

- **`FlightStartCol`**  
  Specifies the name of the column after cleaning, which represents the flight start date.  
  - Common values:  
    - `week-wc` for MediaPlans.  
    - `month-week_-wc` for BlockPlans.

- **`FlightingRowCount`**  
  Indicates the number of rows merged to represent a single plan or actual line item.

- **`PrimaryFlightingConfig`**  
  Defines the row where metrics, such as impressions, are input.  
  - Example: If the impressions metric is in the second row (Python indexing), set `PrimaryFlightingConfig` to `2`.

  |   |   |
  |---|---|
  | Flight Status| xxxxx  |
  | Net Net Cost| 0000.0  |
  | Impression | 000  |

---

### Mandatory and Optional Columns

- **`BaseMandatoryColumns`**  
  Lists columns that are required in the MediaPlan.  
  - Delimited by commas.  
  - Column names must match the `constant.py` replacement dictionary or their post-cleanup names.  
  - Missing columns trigger a **fatal error**.  
  - Ensure these include cost-related columns.

- **`BaseOptionalColumns`**  
  Lists columns that are optional but included if present.  
  - Delimited by commas.  
  - Column names must match the `constant.py` replacement dictionary or their post-cleanup names.  
  - Missing columns generate a **warning**.

---

### Calculation Settings

- **`ZeroCostCol`**  
  Identifies columns containing values like `Flat fee`, `Zero Cost`, `Value Add` to ignore rows with no spend. The column name must reflect its cleaned version.  

- **`RateCalculateCol`**  
  Specifies columns used to calculate cost-per-metric. Two values are required (in order):  
  - The cost column.  
  - The metric column.

- **`ActualRateCalculateCol`**  
  Functions like `RateCalculateCol` but applies to actualisation. These values should reference the actual cost and metric columns (in order).

- **`Actualise`**  
  Indicates whether to process an actualised section for partial actualisation. Accepts `TRUE` or `FALSE`.

---

### Date Settings

- **`MediaPlanYear`**  
  Defines the default year for converting week numbers into `YYYY-MM-DD` format.

- **`DateCol`**  
  Refers to the column containing weekly numbers in the MediaPlan typically in a  `{week number}-{day start}` format -> generally seen like `0-25`  
  - Delimit using `,`
  - There have been workarounds added for specfic MediaPlans for New Balance.

- **`MediaDates`**  
  Names the columns for start and end dates in the MediaPlan. Typically, `start_date, end_date` with the first delimiter as `start` and the second as `end`.

- **`AdditionalDateCols`**  
  Specifies additional date columns to include in the table. Useful for plans with date inputs in the weekly breakdown, which can override `MediaDates`.

---

### Validation

- **`TemplateCheck`**  
  Ensures the template structure is unchanged. For example, adding `Flighting Status, Cost` will validate that each index in `FlightStartCol` contains rows with these values. Missing rows trigger a **fatal error**.

---

### Naming and Errors

- **`FatalNamingCol`**  
  Identifies columns where naming errors result in a **fatal error**. These must also be listed in `BaseMandatoryColumns` and match the `Shared Values` header.  

- **`WarningNamingCol`**  
  Identifies columns where naming errors result in a **warning**. Values not matching the `Shared Values` tab generate a warning.

- **`MetaKeys`**  
  Lists expected values in the meta table’s left-hand side (e.g., `MediaPlan ID`, `Channel`, `FX Rate`). Missing values trigger a **fatal error**

---

### Excel Processor Settings

- **`FinalStartCol`**  
  Specifies the last column to unmerge for processing. Used in the `ExcelProcessor.get_vertical_merge_reference()` function.

- **`FinalStartColType`**  
  Indicates the expected data type for the column specified in `FinalStartCol`.

- **`LineItemDictCol`**  
  Defines the first column with merged cells in the plan. Used in the `ExcelProcessor.extract_lineitem_dict()` function.

- **`BlockplanMetricColumns`**  
  Specifies metric columns in BlockPlans, delimited by commas.

---

### Miscellaneous

- **`NaNColumns`**  
  Specifies columns that, if empty, result in row removal. This will convert the value to a list you do not need square brackets. 
  <br>**The usecase being**  
  ```python
  df.dropna(subset=NaNColumns)
  ```

- **`gold_mediaplan_meta`**  
  Identifies which fields from the bronze table should be pushed into the `gold_mediaplan_meta` table.  
  _Note: This table is currently unused._

