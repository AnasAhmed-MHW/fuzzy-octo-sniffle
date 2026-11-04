---
title: Mediaplans
parent: Value Retail
has_children: true
nav_order: 2
last_modified_date: 2026-10-27 14:00
---

# Mediaplans

Value Retail mediaplans track **offline + online media** that is being bought. Planners fill a standard Excel template, submit via Radar, and Databricks validates then lands the plan into bronze / gold tables used by Canonical, SIGNAL, and MMM.

This section covers the **online Databricks process only**.

```mermaid
flowchart LR
    R[Radar upload] --> I[Ingestion]
    I --> Q[QA]
    Q --> D[Deletion if needed]
```

| Page | What it covers |
|---|---|
| [Ingestion process](ingestion-process) | Radar → S3 → Trigger → Runner → bronze / gold |
| [Successful plan rules](successful-plan-rules) | What the online validator requires for a plan to ingest |
| [QA checklist](qa-checklist) | What to check in Canonical, Radar, and SIGNAL after upload |
| [Deletion process](deletion-process) | Removing wrong plans via the MediaPlan Deletion Notebook |

{: .note }
> After a successful upload it usually takes **~30–60 minutes** for the plan to show in gold tables and the SIGNAL mediaplan dashboard.
