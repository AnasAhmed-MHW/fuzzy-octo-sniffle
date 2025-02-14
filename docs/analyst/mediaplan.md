---
title: MediaPlan Actions
parent: Analyst Engineering Guide
nav_order: 6
last_modified_date: 2025-01-23 12:00
---

# MediaPlan Actions

This guide provides step-by-step instructions for performing common MediaPlan operations.

## Removing MediaPlans

Follow these steps to delete MediaPlans:

1. Open the [MediaPlan Deletion Notebook](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/2229854172572429?o=7058903129942627#command/6484831897324819).
2. Locate the 3rd cell titled `Variables for User to Fill`.
3. Populate the `plans_to_delete` variable with the MediaPlans you want to delete:
   
   ```python
   plans_to_delete: List[str] = [
       "MP2_123",
       "MP2_234",
       "MP2_345",
   ]
   ```
4. Run the next two cells to display dropdown selections:
   - **plan_type**: Choose either `mediaplan` or `blockplan`.
   - **run_env**: Select `prod` or `dev`.
   - **schema**: Select the client. Note: There are two 'value_retail' clients; the first is a demo client for testing.
5. Continue running the cells until you reach cell 8, where MediaPlans are moved from the success/failed folders to the archive folder:
   - If an error occurs here, it likely means the files cannot be found.
6. Run the next cell to delete the MediaPlans from the relevant tables.
7. The final cells will log the removed MediaPlans.

## Rerunning MediaPlans

To rerun MediaPlans, follow these steps:

1. Open the [MediaPlan ReRun Notebook](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/2099578160036880?o=7058903129942627#command/4171076204885338).
2. Run the initial cells until the dropdown widgets appear.
3. Select values from the following dropdowns:
   - **Success or Failed**: Choose whether the last execution of the MediaPlan was successful or failed.
   - **run_env**: Select `prod` or `dev`.
   - **schema**: Choose the client. Again, note that there are two 'value_retail' clients, with the first being a demo client.
4. Populate the `plans_to_rerun` variable with the MediaPlans you want to rerun:
   
   ```python
   plans_to_rerun: List[str] = [
       "MP2_123",
       "MP2_234",
       "MP2_345",
   ]
   ```
5. This process moves the MediaPlan into the `uploads` folder, triggering the MediaPlan workflow to rerun the MediaPlan.


{: .warning}
Running an Inactive MediaPlan (with a different MediaPlan Name and the same MediaPlan ID) will overwrite the data for the current active / latest MediaPlan