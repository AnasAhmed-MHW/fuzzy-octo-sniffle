---
title: Join & outputs
parent: Non-Media Data Processing
grand_parent: MMM Data Processing
nav_order: 9
last_modified_date: 2026-10-28 09:50
---

# Join & outputs

How all Non-Media sources combine onto the FF & Sales spine and what gets written out.

## Shared helpers (notebook)

| Helper | Role |
|---|---|
| `iso_week_year_to_date` | ISO week + year → Monday date |
| `week_str_to_date` / conditional variants | Partnerships strings like `Week 52 21` → date (+7 day offset except week 53 24) |
| `village_code_to_name` / `village_mapping_2` | BV↔Bicester Village style maps |
| `map_country_village` | PR Domestic / International / Ignore |
| `Partner_segment_to_variable` | Partnership segment → `_Corporate_Other`, `_Mobility`, etc. |
| `map_campaign_to_group` | Email campaign → Membership, Retargeting, Newsletter, etc. |

Week grain is consistently **week commencing Monday**.

---

## Footfall & Sales (join spine)

| | |
|---|---|
| **Table** | `prod.value_retail.gold_mmm_ffandsales` |
| **Role** | **Primary spine** for the master join |
| **Built by** | [FF and Sales Data Processing](../ff-and-sales-data-processing) |

Selected fields include total sales, footfall, members, domestic/international member sales & footfall, and adjusted non-member footfall/sales — then pivoted wide by `village_name` on `week_commencing_monday`.

{: .important }
> Every other source is left-joined onto this FF & Sales frame. Weeks without FF/Sales do not appear in the final output.

Also referenced for exploration: `raw.value_retail.village_daily_performance` (SQL select only; not in the final join).

---

## Naming conventions

| | |
|---|---|
| **Path** | `s3://mh-rawdata-valueretail/mmm/naming_conventions/` |
| **Filter** | `Status != 'Not Mapped'` |

Not a feature source — maps `Original_Column` → `Mapped_Column` so village extracts use MMM-standard names before Delta write.

---

## Master join (`final_joined_df`)

Left-join order onto `pivoted_ff_sales` (alias `ff`):

| Alias | Source pivot | Join condition |
|---|---|---|
| `pr_social` | PR Social | `ff.Week_Commencing_Monday` = `Week_Commencing` |
| `online` | PR Online | same |
| `pr_print` | PR Print | same |
| `org_soc` | Organic Social | same |
| `search` | Organic Search | = `Week_Start_Date` |
| `website` | Website | = `Week_Start_Date` |
| `gt` | Google Trends | = `Modelling Week_gt` |
| `me` | Marketing Events | = `ME_Date` |
| `occ` | Occupancy | = `Week_Commencing` |
| `pt` | Partnerships joined | = `Week_Start_Date` |
| `oecd` | OECD | = `week_commencing_monday` |
| `email` | Email | = `Week_Commencing` |
| `hol` | Holidays | = `Week_Commencing` |
| `weather` | Weather pivot | = `date` |

Spaces in column names are then replaced with underscores. Result: one wide weekly row with FF/Sales KPIs plus all non-media features.

---

## Village extracts

| Village | Filter cues | Output |
|---|---|---|
| Bicester (BV) | `bv`, `bicester_village` | **Written** → `dev.value_retail.non_media_bv` |
| Fidenza (FV) | `fv`, Fidenza | Display only |
| Ingolstadt (IV) | `_iv_`, Ingolstadt (+ shared DE macro cols) | Display only |
| Belmont Park (BP) | `BP`, Belmont Park | Display only |
| Kildare (KV) | `KV`, Kildare, `kil_` | Display only |
| La Roca (LR) | `LR`, La Roca, `ph_esp`, `ph_lr_` | Display only |
| La Vallée (LV) | `LV`, La Vallee, `ph_lv_`, `sch_lv` | Display only |
| Las Rozas (LZ) | `LZ`, Las Rozas, `esp`, `ph_lz` | Display only |
| Maasmechelen / Wertheim | — | Cells commented out |

For BV (and several others), naming-convention renames are applied, then Delta-friendly lowercasing / special-character cleanup before write.

---

## Output artefact

| Artefact | Detail |
|---|---|
| **Table** | `dev.value_retail.non_media_bv` |
| **Format** | Delta (`overwrite`) |
| **Grain** | One row per `Week_Date` (Monday) |
| **Contents** | BV FF/Sales KPIs + BV-scoped non-media features with mapped names |

{: .tip }
> Re-run Non-Media after refreshing S3 CSVs or upstream FF/Sales / [weather](weather) / [OECD](oecd) tables.

{: .warning }
> S3 file names are brittle (spaces, typos, trailing spaces). Updating a source usually means changing the `FILE_*` constant in the corresponding notebook cell.
