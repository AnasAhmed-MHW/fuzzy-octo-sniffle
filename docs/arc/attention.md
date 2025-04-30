---
title: attention
parent: ARC
last_modified_date: 2025-04-30 12:00
---


ARC is when we use the Lumen attention data in order to create a bidlist + whitelist which we attach to the adgroup for targeting.

ARC repo currently only works on the DataOps Shared Compute Cluster. API secret keys and secret login details are stored on this cluster only. 

## Tradedesk - running a new campaign with ARC

With ARC Tradedesk campaigns we attach both a bidlist and a whitelist when running campaigns.


1. Open up [bidlist_creation_tradedesk](https://dbc-341b6afb-df67.cloud.databricks.com/?o=7058903129942627#notebook/422650837981582/command/964520352917585) and add an entry in the dictionary similar to below:

```

"Epidemic Sound Banner": {
    "ACCOUNT_NAME": "Epidemic Sounds (IPG | Mediahub)",   # From Lumen dataset (hive_metastore._global.bronze_lumen_attention, column name is account_name)
    "ADVERTISER_ID": "3slmhsj",                           # From Tradedesk
    "CAMPAIGN_TYPE": "Banner",                            # Banner or Video
    "AD_GROUPS": ["qxgn62f", "ufhtnmg", "18k012b"],       # From Tradedesk, also provided by Kinesso team
    "BIDLISTS": ["388907558"],                            # Result from create_bidlist_domain_only() function. Keep it an empty you run function. If not needed leave it like [] or [""]
    "WHITELISTS": ["396302267"],                          # Result from create_whitelist() function. Will be black until you run function. If not needed leave it like [] or [""]
    "BASE_BIDS": 1,                                       # From Tradedesk, also provided by Kinesso team. Currency is already set in the adgroup
    "MAX_BIDS": 10.08,                                    # From Tradedesk, also provided by Kinesso team. Currency is already set in the adgroup
    "DATE_FILTER_MIN": "2024-01-01",                      # From Tradedesk, also provided by Kinesso team
    "DATE_FILTER_MAX": "LATEST",                          # Can filter by today’s date or earlier
    "APM_FILTER": 600,                                    # Adjust as needed; 600 APM is good for Banner campaigns on Tradedesk, 1000 APM is good for Video on Tradedesk
    "IMPRESSIONS_FILTER": 10,                             # Adjust as needed; helps balance high APM and low impressions
    "KINESSO_INCLUSION_BIDLIST": "5152024"                # Standard whitelist of many domains that's added to every adgroup. You can get this from the Kinesso team. If not needed, leave blank or ""
}
```

2. The action dropdown contains the actions test, create, refresh, attach, create and attach. Select "create and attach" in the action dropdown: 

![screenshot 1](https://lh3.googleusercontent.com/pw/AP1GczMeFlisvoyNrgvY29ltdCB2h52kcyDgTm_J7-jZMWHqvRVPKARzTfrJme_eaDiT7DHmhdPZHMmkix0OSWhzBVsJidI6Kts_YmeP1GuPMLHnV3dopUKq3OfeR4kDOGafTnlrMDg9sAOaiVf4uZ7n_JTl=w186-h210-s-no-gm?authuser=0)

3. Run the whole [bidlist_creation_tradedesk](https://dbc-341b6afb-df67.cloud.databricks.com/?o=7058903129942627#notebook/422650837981582/command/964520352917585) notebook.

4. You should receive a Bidlist ID and a whitelist ID. Put those in the dictionary as values for the campaign you're running in the keys "BIDLIST" & "whitelist" respectively. 

You should see the message "Have successfully attached bidlist 1234567 to adgroup abcdef" which means the bidlist is now ready. It will be refreshed every Monday. This is the [workflow](https://dbc-341b6afb-df67.cloud.databricks.com/jobs/612427242814961?o=7058903129942627) that runs the bidlist refresh.

Also within the Tradedesk platform at the Ad Group level, you should see the message "API Settings applied, the bidlist added in the Site/App as an optimisation, and the changes added to the Activity Log:

![screenshot 1.1](https://lh3.googleusercontent.com/pw/AP1GczOuvX6FT2OF5ikYWi4jQAsoMj6Uu6OBs80aDYkZlBdXCOrx2yl4-AhNKgF5c0qHaJDE2I3D2sONb6BxDOQJdmXwCSC6UoGcyti27TGU9-jY-owH4AcIZN3jkJuR4bxpyME2Wr7yBE6v-De3QuutqQBx=w1902-h884-s-no-gm?authuser=0)
![screenshot 1.2](https://lh3.googleusercontent.com/pw/AP1GczNaZI7Zk0I9NnLclFU6naHqmmXDlLel99SMSEhX_gbqJBZVgGXXvbQe36BwQ8q1Jku5qgdASKMLf4HcX9XPH8K8JemxbtXE1fo5w51FYNjzuX5YZpyPcT0ZVlC0C5Q3xlIJpGsMOUBc-Jz-f4G-3UxK=w1795-h542-s-no-gm?authuser=0)
![screenshot 1.3](https://lh3.googleusercontent.com/pw/AP1GczNyqugXMm1r4NmUYYF6HZzT1vWm8cfIXeVBseeqWH_CV9zTf8-gypluYqnwa2_ba7kRqpVg6FICW3ksXoJHCtwSgresFos-VV-C6desTudkClo6fmx5CUJxIcu9Ksy6ubCf1quKSiuKMeveHl2yPdjn=w1026-h845-s-no-gm?authuser=0)

You can also use the create & attach actions seperately in order to achieve the same thing, or if you wanted to create a bidlist but have yet to recieve adgroups to attach the bidlists to.

## Tradedesk - manually refreshing a bidlist for a current campaign with ARC

To refresh a campaign we are currently running, follow these steps:

1. The action dropdown contains the actions test, create, refresh, attach. Select "refresh" in the action dropdown and add a name to the whitelist you want to add too: 

![screenshot 2](https://lh3.googleusercontent.com/pw/AP1GczNSV21Gp7F6LobfX9jF34OotlyLH47kECWagE1I5_cv8P6wBgA4pw4iax91J-UY1aKg3IVjgUp7a7X8QXF6CoutBB_lIeLLwB1_pMDcnTjoYrHnmmdh4iNy1ggA_JoDSF4UIZDHeE2Cb2tygIHljuQ=w170-h170-s-no-gm?authuser=0)

2. Run the whole [bidlist_creation_tradedesk](https://dbc-341b6afb-df67.cloud.databricks.com/?o=7058903129942627#notebook/422650837981582/command/964520352917585) notebook.

The bidlist should be refreshed and you'll see the message: Have successfully updated bidlist 1234657.


## Tradedesk - Video Player Size

For all video ad groups, we reccomend always blocking small player size within the DSP. Time and time again, we have seen that small player size placements have low APM and should therefore be blocked like so:

![screenshot 2.1](https://lh3.googleusercontent.com/pw/AP1GczOe-VGFQQQUaZUC4M3Ih5-GdRDYerhQZxygyi-mCGfRaSslZ7Zz5B3YHAjPyGZHFdwyGroj2-5ovF6T6Gi14b68od-99V55mmrGix7R9Q5mE4wIKlBuMn4YpFPD98uUrlU944xv2uVmv-1_i7tEHt2f=w2336-h1088-s-no-gm?authuser=0)


## Yahoo DSP - running a new campaign with ARC

For the Yahoo ARC campaigns, we add both a bidlist and a whitelist just like we do on Tradedesk.

1. Open up [bidlist_creation_yahoo](https://dbc-341b6afb-df67.cloud.databricks.com/?o=7058903129942627#notebook/422650837981583/command/964520352917592) and add an entry in the dictionary similar to below:

```

DICT_LIVE_CAMPAIGNS = 
    "AkzoNobel Banner": {
        "ACCOUNT_NAME": "Epidemic Sounds (IPG | Mediahub)",   # From Lumen dataset (hive_metastore._global.bronze_lumen_attention, column name is account_name)
        "CAMPAIGN_TYPE": "Banner",                            # Banner or Video
        "AD_GROUPS": "3389020",                               # From Yahoo (called Lines), also provided by Kinesso team
        "BASE_BIDS": 1,                                       # From Yahoo, also provided by Kinesso team. Currency is already set in the adgroup
        "MAX_BIDS": 10.08,                                    # From Yahoo, also provided by Kinesso team. Currency is already set in the adgroup
        "DATE_FILTER_MIN": "2024-01-01",                      # From Yahoo, also provided by Kinesso team
        "DATE_FILTER_MAX": "LATEST",                          # Can filter by today’s date or earlier
        "APM_FILTER": 600,                                    # Adjust as needed; good APM is currently unknown for Yahoo DSP
        "IMPRESSIONS_FILTER": 10                              # Adjust as needed; helps balance high APM and low impressions
}
```

2. The action dropdown contains the actions test, create and attach, refresh. Select "create and attach" in the action dropdown: 

![screenshot 3](https://lh3.googleusercontent.com/pw/AP1GczOEyJ6Ua04KTMcOxRn-98mOPcZe2pHAkmh9SW4ZDtmnvnFFArKjelC7KsTgLR26G9Pd6X6af8lEnsW0GDLi2gATEs2LDr047vP-tr-uW6OCz4Q2rUim2xxu86Z0dKJn5YrQKJ189qeLV4LxCQsTA23o=w382-h137-s-no-gm?authuser=0)

3. Run the whole [bidlist_creation_yahoo](https://dbc-341b6afb-df67.cloud.databricks.com/?o=7058903129942627#notebook/422650837981583/command/964520352917592) notebook.

You should see the message: "Created bidlist for Line ID 1234567." The bidlist is now be ready to be refreshed every Monday. As you may have noticed, there is no need to attach the bidlist as each bid multiplier is attached to the Yahoo AdGroup (AdGroups are referred to as Lines in the Yahoo DSP). This is the [workflow](https://dbc-341b6afb-df67.cloud.databricks.com/jobs/612427242814961?o=7058903129942627) that runs the bidlist refresh every Monday.


Also within the Yahoo platform at the Line/Ad Group level, in the Bid Multipliers Apps & Sites section, you should the URLs and bid multipliers added to the platform. Sometimes it takes a few hours to appear in the UI:

![screenshot 3.1](https://lh3.googleusercontent.com/pw/AP1GczP_7JLYE5fL56g_Ek1vSjacftfp8CPfIkwZX5I76lDTlxbK41Kaio5HcdXAJXVd2pSvpr7A3zDGvULYbEALNgbfcIjoRZqxQFG6MjIB8eK3lFwuA3qfQ1hDjfHY24G7Jn_kTn8eO8GKRQorRm04EcaZ=w1906-h711-s-no-gm?authuser=0)

To see if the bidlist has been attached faster, use the get_bidlist function:


```python

sys.path.append(os.path.abspath('/Workspace/Repos/krishan.vadher@mediahubww.com/datastream_api'))
from datastream_api.yahoo import api_yahoo
client_id = dbutils.secrets.get(scope="yahoo_mediahub_us_krishan", key="client_id")
client_secret = dbutils.secrets.get(scope="yahoo_mediahub_us_krishan", key="client_secret")
class_actions = api_yahoo.Actions(client_id, client_secret)

data = class_actions.get_bidlist(ENTER_LINE_ID)

print (data)

```
## Yahoo - adding the whitelist

You also need to manually attach the whitelist that has been created. Yahoo DSP does not allow you to programmatically attach whitelists to adgroups. To do this: 

1. Navigate to the Yahoo DSP adgroup you want the whitelist attach to:

![screenshot 6](https://lh3.googleusercontent.com/pw/AP1GczO74ywn_WRRBR1sGT8cdtcArdp5hFGLMLGF7p3vnjFBc8BZm9bVzf_KjYESdQzbgoivxepfPFV4ua0QhL15031yeu8lw8VkUPxCssOUAns7e-kmbLIULCFWDaUwXHubvzLE1j8J78aB720xGaZ0nAOv=w2530-h966-s-no-gm?authuser=0)

2. Click on App & Site Lists and select the whitelist you have created on the dropdown.

![screenshot 7](https://lh3.googleusercontent.com/pw/AP1GczOhZCbxbMZIvZhOtyoBX4DozUwa99gwWIOiIWIUkUcQ81I4IHbrvJnM7-2gKu41GhosVMfUO-e64UQrGdl9Rc3l9kJkZqOexWa1YLOb7xWh6XJeOrAmviALXtndgczDpPJgGLyYup8_yjNqJfP6nqVM=w1788-h1081-s-no-gm?authuser=0)

## Yahoo - manually refreshing a bidlist for a current campaign with ARC

To refresh a campaign we are currently running, follow these steps:

1. The action dropdown contains the actions test, create, refresh, attach. Select "refresh" in the action dropdown: 

![screenshot 4](https://lh3.googleusercontent.com/pw/AP1GczN20thiWse8jL-oh_r2OlLCdgFFA-XUUHdhko2malyoZiZJ_qYXjBxKZ-Rkgswj97bDlFXkqzkG5yt9ZPVPa1iKe9vailg1C3KkvdloC5WqskR0o4aGfgpU2qkY6z21wlUZsag4Cr5q_BFav6M8qhI=w186-h146-s-no-gm?authuser=0)

2. Run the whole [bidlist_creation_yahoo](https://dbc-341b6afb-df67.cloud.databricks.com/?o=7058903129942627#notebook/422650837981583/command/964520352917592) notebook.

The bidlist should be refreshed and you'll see the message: Bidlist refreshed for Line ID 1234567.

## Tracking what campaigns are live

To track which campaigns are currently live, placement ids, links to adgroups, use the following [Google Sheet](https://docs.google.com/spreadsheets/d/1UZ7URe3N72xXTxPn-CsrtumanecjJ9ng6lfS-5waM48/edit?gid=0#gid=0).

## Notes on Yahoo DSP

With bidlists, bid multipliers cannot be deleted with the API once they have been uploaded. You will have to change the bid multiplier to 0 in order to not serve on domains you would ideally like to delete.

## FAQS

1. Question: What if APM is not high? Answer: The best way to raise APM is by making the bidlist smaller and smaller, even to the detriment of pacing. Once APM is to an acceptable level, feel free to make the bidlist bigger again in order to meet pacing targets.
2. Question: How do we usually structure test and control campaigns from a bidlist perspective? Answer: The test should have both a bidlist and a whitelist attached to it from ARC. The control shouldn't have any ARC bidlists or whitelists. The control is helpful in order to pull in new domains which can be added to test if they show to have good performance. 
3. Question: What is generally a good benchmark for APM regardless of advertiser? Answer: For Tradedesk display campaigns, 600+, for Tradedesk video campaigns 1000+. For other DSPs, we have not ran enough ARC campaigns.
4. Question: What are the steps to add a new client? Answer:

    4.1. Get UI access to the new client on the DSP they will be running the campaign on

    4.2. Get API access to the new client on the DSP

    4.3. Check that you can read and write to the clients account on the DSP (test by using get_adgroup() & attach_bidlist_to_adgroup() functions)

    4.4. Check in the table hive_metastore._global.bronze_lumen_attention that we get Lumen attention data

    4.5. If we don't send a message to our current Lumen representative (currently alexander.harrington@lumen-research.com)

    4.6. Create a bidlist to test and see if the pipeline works end to end  

## Dashboard

A dashboard is available [here](https://dbc-341b6afb-df67.cloud.databricks.com/sql/dashboardsv3/01ef9b7b05d9150e8fab85345d3956c5?o=7058903129942627) in order to monitor performance and the state of th eLumen data pipeline.

## Notes

- All data informing ARC campaigns comes from the bronze_lumen_attention dataset whih is a joined dataset of all the client Lumen data found [here](https://eu-west-1.console.aws.amazon.com/s3/buckets/mh-lumen-attention?region=eu-west-1&bucketType=general&tab=objects) (example file name: MH_S3_Clients_2024-11-10T1401_ddrRFf.csv)
- Bidlist, Custom Algorithm, Algorithm all mean the same thing with ARC.
- Remove campaigns from DICT_LIVE_CAMPAIGNS when campaigns are no longer live.
- Keep an eye on Ad Group Health in order to see what may be effecting pacing the most. It lets you know how much the ARC bidlist/whitelist may be effecting the ad group:

![screenshot 5](https://lh3.googleusercontent.com/pw/AP1GczOXQnHdPbPvYJPSjK4cN4FvcdWjbY3ZGJPzj0GIrld8HGVAqhDOzI13vzfKcc5selIklGU4QZawxOu2I_KqiKan-zIuAQUTsL1A4zMCcmClXX8SjWEEYEIew-gDwcQxKwiH48DeJiU9BaLrocYqkecy=w958-h432-s-no-gm?authuser=0)
- Have found that bidlists have not refreshed/pipelines broken because of changes made on Lumens side to the dataset. Check these especially if there is an ongoing ticket/dispute over our data pipeline.
