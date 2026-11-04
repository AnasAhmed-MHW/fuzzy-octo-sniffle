---
title: Successful plan rules
parent: Mediaplans
grand_parent: Value Retail
nav_order: 2
last_modified_date: 2026-10-27 14:00
---

# Successful plan rules

What the online Main MediaPlan Notebook requires for a plan to ingest. Bronze write only happens when `canonical.fatal_error == False`. **Warnings still ingest**; fatals block the whole file.

Always cross-check formats against the [Governance Inputs sheet](https://docs.google.com/spreadsheets/d/1rYsIpscgFCDN_YX6TnDEp9ZCfm_C8O_CZ1pZNv25n04/edit?gid=1900709516#gid=1900709516) — **MediaPlan**, **Shared values**, and **FeildCodes** tabs. If a value is missing from Shared values, ask D&A to add it rather than free-typing a close variant.

---

## Hard requirements before upload

1. **Correct template version** — filename must start with `MP[n]_` (Value Retail currently supports up to **MP7**). Version in MediaPlan Info must match.
2. **Save as real Excel** — `.xlsx` workbook (not CSV / broken export).
3. **Valid channel sheets** — expected tabs present; missing *all* valid sheets is FATAL.
4. **MediaPlan Info complete** — labels/values between Meta SkipRows → SkipRows; required meta filled; dropdown meta fields ∈ Shared values (`MetaKeys to Check`).
5. **One MediaPlan ID** across every sheet (different IDs = FATAL).
6. **Mandatory / NaN columns** present and filled on every active line item.
7. **Taxonomy / dropdowns** — line-item columns listed in Gov `FatalNamingCol` must match Shared values exactly (trim + case-insensitive). Unknown values → FATAL. `WarningNamingCol` mismatches warn but still ingest.
8. **Spend ↔ Primary KPI pairing** — both filled or both empty (zero-cost rows exempt where configured). Non-numeric values FATAL.
9. **Weekly flighting** — weekly KPI sum must not be 0 on active rows; weekly date headers valid (`dd/mm/yyyy` or `dd mmm yyyy`); flighting block matches template.
10. **No duplicate column headers**; start ≤ end dates (reversed dates are WARNING — plan can still ingest).

---

## Fatal vs warning

| Level | Blocks bronze? | Typical causes |
|---|---|---|
| FATAL | Yes | Missing template cols, empty mandatory cells, bad fatal taxonomy, spend/KPI mismatch, weekly KPI = 0, bad week dates, multiple MediaPlan IDs |
| WARNING | No | Soft taxonomy (`WarningNamingCol`), some date start/end issues, partial missing sheets |

Planners see these outcomes in [Canonical](https://prod.d2oohu4fo82r82.amplifyapp.com/valueretail/apps/canonical) after the [ingestion process](ingestion-process) runs.

{: .warning }
> **Known VR MP7 Gov issues:** `MediaDates` is unset for MP7 — online ingest can fail with a config/`KeyError` even when the Excel looks fine (fix belongs in Governance Inputs, not the template). `PrimaryFlightingConfig` may be off-by-one so “Weekly KPI totaling to 0” can point at the wrong Excel row in Canonical.
