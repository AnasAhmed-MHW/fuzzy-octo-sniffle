---
title: Versioning
parent: Media Investment Data
grand_parent: MMM Data Processing
nav_order: 1
last_modified_date: 2026-10-28 09:55
---

# Versioning

Every time mediaplans change in gold, MMM keeps an **immutable snapshot** in `dev.value_retail.gold_mediaplan_versioned` (Delta, partitioned by `version_id`) so prior modelling cuts can be reproduced.

## Tables

| Table | Role |
|---|---|
| `hive_metastore.value_retail.gold_mediaplan` | Live gold mediaplan (upstream ingest) |
| `dev.value_retail.gold_mediaplan_versioned` | Append-only history; each snapshot has `version_id` + `dt_created` |

---

## Workflow in the notebook

### 1. One-time table create (do not re-run)

Creates `gold_mediaplan_versioned` from the first gold pull as `version_id = 1` (cell is wrapped so it is not re-executed casually).

### 2. Build the next version (run when cutting a new MMM snapshot)

```sql
CREATE OR REPLACE TEMPORARY VIEW gold_mediaplan_next_version AS
WITH max_version AS (
  SELECT max(version_id) AS version_id FROM dev.value_retail.gold_mediaplan_versioned
)
SELECT *, (SELECT version_id FROM max_version) + 1 AS version_id, current_timestamp() AS dt_created
FROM hive_metastore.value_retail.gold_mediaplan
WHERE sourceglobal_partner != "theTradeDesk";
```

{: .important }
> **Trade Desk / TTD rows are excluded** from new version inserts. Display for MMM is taken from **API / SIGNALDATA** instead of manually ingested Trade Desk mediaplan lines (comment in notebook).

### 3. Insert into the versioned table

```sql
INSERT INTO dev.value_retail.gold_mediaplan_versioned
SELECT * FROM gold_mediaplan_next_version;
```

This **appends** — it does not overwrite older `version_id`s. Downstream cells typically use:

```sql
WHERE version_id = (SELECT MAX(version_id) FROM dev.value_retail.gold_mediaplan_versioned)
```

### 4. Delete a bad version (only if needed)

Commented helper in the notebook:

```sql
-- DELETE FROM dev.value_retail.gold_mediaplan_versioned WHERE version_id = <n>
```

Use only when a mistaken snapshot must be removed; prefer fixing forward with a new version when possible.

---

## Why this matters

| Benefit | Detail |
|---|---|
| Audit trail | Every MMM cut has a `version_id` + `dt_created` |
| Reproducibility | Re-run mapping / exports against a fixed version instead of drifting live gold |
| Safe iteration | Mediaplan re-uploads in Radar update live gold; versioned table keeps the cut used for modelling |

{: .tip }
> After Radar mediaplan changes land in `gold_mediaplan`, run **next version → insert** before regenerating MMM media exports so the change is recorded.
