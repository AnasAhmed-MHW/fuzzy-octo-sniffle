---
title: QA checklist
parent: Mediaplans
grand_parent: Value Retail
nav_order: 3
last_modified_date: 2026-10-27 14:00
---

# QA checklist

What to check after a plan has gone through the online [ingestion process](ingestion-process).

## Key links

| Resource | Link |
|---|---|
| Canonical | [Canonical dashboard](https://prod.d2oohu4fo82r82.amplifyapp.com/valueretail/apps/canonical) |
| Radar | [Value Retail Radar](https://prod.d2oohu4fo82r82.amplifyapp.com/valueretail/radar#) |
| SIGNAL mediaplan report | [Client Portal report](https://prod.d2oohu4fo82r82.amplifyapp.com/valueretail/apps/signal/reports/3607c9bb-2a9d-49b9-9d1f-b067457690a2) |

{: .note }
> Gold / SIGNAL can lag **~30–60 minutes** behind a successful Radar upload. Wait before assuming failure and re-uploading.

---

## In Canonical / Radar

- Confirm the plan shows **SUCCESS** (not FAILED / not ingested).
- Open error detail rows — Canonical flags taxonomy, incomplete input, invalid template, date errors, etc.
- If Radar says success but SIGNAL is empty, wait out the gold lag first.

---

## In SIGNAL / gold numbers

- Village, channel, and buy-type taxonomy look right vs the Excel.
- Spot-check weekly spend / KPI totals against the uploaded file (ingestion does not fail a plan solely because a line-item total disagrees with its weekly grid — verify manually in SIGNAL).
- Date formatting mistakes (especially regional Excel date settings) often produce wrong Radar/gold figures even when the file “succeeds”.
- Recurring planner issues: wrong date formats → bad figures; failed Radar uploads needing reupload; channel misclassification (e.g. programmatic vs display).

---

## Quick checklist

<details markdown="block">
<summary>Planner / analyst checklist</summary>

- [ ] Filename `MP[n]_…` and Version in Info match current template
- [ ] All required channel sheets present
- [ ] Single MediaPlan ID on every sheet
- [ ] Meta + line-item dropdowns match Shared values
- [ ] Mandatory / NaN columns filled on active rows
- [ ] Spend and Primary KPI both filled or both empty; numeric
- [ ] Weekly breakdowns non-zero where expected; dates `dd/mm/yyyy` or `dd mmm yyyy`
- [ ] After upload: Radar success → Canonical clean → SIGNAL figures match Excel (~30–60 min)

</details>

If the plan ingested incorrectly and must be removed, see [Deletion process](deletion-process).
