---
title: Workflow
parent: RADAR
nav_order: 4
last_modified_date: 2024-06-20 12:00
---

# The Databricks Workflow

The MediaPlan workflow is split into 2 different workflows. 

1. The `TRIGGER`
   This runs multple notebooks. 
   1. The Trigger Notebook. - The trigger notebook has a threadpool executor that can run the same notebook concurrently with different variables
   2. The Update Noteboko - This ensures the latest mediaplan is falgged as active and the mediaplan name x mediaplan id is consistent.
   3. The Gold Notebook - If there are gold tables for the client the gold notebook is added to the end of the workflow

2. The `RUNNER`
   This runs the `Main Notebook` for the mediaplan - this will take the variables:
   - Filename
   - Client 
   - Run env
  
This set up allows multiple notebooks to run concurrently and the `RUNNER` workflow allows you to track failed and successful runs easier. 

{: .important}
You will need to reference the runner workflow in the configs. 

