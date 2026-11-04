---
title: Deletion process
parent: Mediaplans
grand_parent: Value Retail
nav_order: 4
last_modified_date: 2026-10-27 14:00
---

# Deletion process

When a plan was ingested incorrectly (or must be removed), use the Databricks deletion notebook rather than hand-editing Delta.

{: .important }
> Notebook: [MediaPlan Deletion Notebook](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/2229854172572429?o=7058903129942627)  
> Path: `/Repos/PROD/MediaPlan/MediaPlan Deletion Notebook`  
> Object ID: `2229854172572429`

---

## How to run it

1. Open the notebook. If widgets are missing, **run once** so they appear, then set values and run again.
2. Set widgets:
   - `plan_type` — `mediaplan` or `blockplan`
   - `run_env` — `prod` or `dev`
   - `schema` — e.g. `value_retail`
3. Fill `plans_to_delete` with **exact** filenames, for example:

```python
plans_to_delete: List[str] = ["MP7_SOME_PLAN.xlsx", "MP7_ANOTHER.xlsx"]
```

4. Run all cells. The notebook will:
   - Archive matching files in the S3 mediaplans bucket (`MediaPlanSort.archive_plan_without_id`)
   - Delete rows from backend tables via `DeletePlans`
   - Display the delete logging table (`ORDER BY end_time DESC`) so you can confirm the deletion

{: .warning }
> Filenames must match exactly. Wrong `schema` / `run_env` will delete against the wrong metastore or bucket (`mh-mediaplans` vs `mh-mediaplans-dev`). Production VR removals use `prod` + `value_retail`.

After deletion, re-upload a corrected plan through Radar and re-check Canonical / SIGNAL ([ingestion process](ingestion-process), [QA checklist](qa-checklist)).
