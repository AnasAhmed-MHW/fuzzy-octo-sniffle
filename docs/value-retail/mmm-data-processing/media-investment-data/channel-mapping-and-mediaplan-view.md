---
title: Channel mapping & mediaplan view
parent: Media Investment Data
grand_parent: MMM Data Processing
nav_order: 2
last_modified_date: 2026-10-28 09:55
---

# Channel mapping & mediaplan view

Turns versioned gold mediaplan rows into MMM-ready spend variables (`Meta_Domestic_spend`, `Display_DSP_Destination_spend`, `TikTok_Domestic_Spend`, etc.).

## Channel mapping tables

| Table | Role |
|---|---|
| `dev.value_retail.mp_channel_mapping_using_MMM` | Static VALUES list rebuilt in the notebook (`media_variable_raw` → `media_variable_clean`) |
| `dev.value_retail.mp_channel_mapping_auto` | Mapping used by the processed MMM view and mapping-checker cells |

Raw keys look like:

`{media_channel}_{media_activity}_{partner}_{audience}`  
e.g. `SOCIAL_PAID SOCIAL_TikTok_DOMESTIC` → `TikTok_Domestic_Spend`  
e.g. `SEARCH_PAID SEARCH_Google Ads_DOMESTIC` → `Search_Domestic_spend`

Direct deals get a `Direct_` prefix on the join key. Mapping covers Display DSP, Search, Meta, TikTok, Snapchat, YouTube, PMax, OOH, TV/CTV, audio, print, native, sponsorships, and Direct_* variants.

{: .tip }
> Mapping-checker cells flag `join_key` values with **no** clean map (`media_variables_map` null). Add those keys to the mapping table before locking an MMM cut.

---

## Join key rules (`gold_mediaplan_versioned_MMM`)

Built from the **latest** `version_id` only:

| Condition | Join key pattern |
|---|---|
| `buying_agency = 'Direct Deal'` | `Direct_{CHANNEL}_{ACTIVITY}_{partner}_{AUDIENCE}` |
| Display + `mediaplan_id = 'SIGNALDATA'` and audience null | `DISPLAY_DISPLAY_{partner}_{DOMESTIC\|DESTINATION}` inferred from `placement_adset_name` |
| Default | `{CHANNEL}_{ACTIVITY}_{partner}_{AUDIENCE}` |

Then left-join to `mp_channel_mapping_auto` on `join_key = media_variable_raw`.

### Source tag

| `mediaplan_id` | `source` |
|---|---|
| `SIGNALDATA` | **API** |
| Anything else (Excel mediaplan) | **MP** |

### Spend tweaks in the view

- Prefer `spend_eur` (with village-specific zero-outs for some historical Trade Desk rows on Maasmechelen / Fidenza).
- Keeps `spend_gbp`, impressions, clicks, village, week Monday, media plan name, channel, agency, partner, local partner, `version_id`.

---

## Downstream uses of this view

| Use | Detail |
|---|---|
| Village / date exports | Filter `gold_mediaplan_versioned_MMM` by village and date window |
| Wide pivot | PySpark pivot on `media_variables_map` summing spend EUR/GBP by day × week × village |
| API biddable slice | Rows with `source = 'API'` and Display / TikTok / YouTube / Performance Max — see [Search, Social & API](search-social-and-api) |

{: .note }
> Trade Desk partner lines are largely **out of new versions**; Display investment for MMM is expected from **API / SIGNALDATA** rows tagged `source = 'API'`.
