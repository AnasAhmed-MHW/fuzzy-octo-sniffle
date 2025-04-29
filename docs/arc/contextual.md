## ARC Contextual

Arc Contextual is when we target by a page url level for display campaigns. You can't directly plug page level url's into Tradedesk or Yahoo DSP. You have to do it through an affiliated third party like Peer39.

ARC repo currently only works on the DataOps Shared Compute Cluster.

## General ARC Contextual Process

flowchart LR
    A[Peer39<br/>Send Page URLs] --> B[S3 Bucket<br/>Store Raw URLs]
    B --> C[Databricks<br/>Filter & Process URLs]
    C --> D[Peer39<br/>Receive Filtered URLs]

    %% Contextual notes
    A:::source
    B:::storage
    C:::processing
    D:::destination

    classDef source fill:#E0F7FA,stroke:#00796B,stroke-width:2px;
    classDef storage fill:#FFF3E0,stroke:#F57C00,stroke-width:2px;
    classDef processing fill:#E8F5E9,stroke:#388E3C,stroke-width:2px;
    classDef destination fill:#E1F5FE,stroke:#0288D1,stroke-width:2px;

## S3 Bucket

Currently the URLs go to this bucket here. When settting up a new campaign, it would be best to receive those files in a new folder in the bucket: 

https://us-east-1.console.aws.amazon.com/s3/buckets/p39-prod-feedout-mediahub

## Databricks Notebook & Workflow

This is the notebook that runs ARC Contextual: 

https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/1070495127561986?o=7058903129942627#command/6120987330216781

There may be more then one workflow to run an ARC Contextual campaign. For example, currently for Kraken this is the workflow: 

https://dbc-341b6afb-df67.cloud.databricks.com/jobs/1456621986298?o=7058903129942627

### Get URLs process

The get_urls.py script gets the urls from the S3 bucket, processes them and creates a tier list depending on how we want to segment and target with our data.

### Push URLs process

The push_urls.py script gets the urls from a processed table (for Kraken for example hive_metastore.kraken.bronze_contextual_arc_kraken_processed) and pushes them to the Peer39 Segments


## When setting up a new Peer39 campaign

You need to first create the segments in the Peer39 platform

With ARC Tradedesk campaigns we attach both a bidlist and a whitelist when running campaigns. Login details can be found in the bitwarden. You need to go to this site: https://app.peer39.com/manage and set up a segment like so and copy the category ID:

[peer39](https://lh3.googleusercontent.com/pw/AP1GczNcSp3JcC5_WeqWZPrbsXzsEbHlIzXLJTyVbmPH-MhPYCr-0DUE9GXpepPGV9FM7j9rFH3FA-g9x8BFdeCs89sSiA6_kRChufzr7qbKw81Gu-7-_jGUSWZZue6gc-oYCvn9Yh3-y8I2fVPj0oz2erjS=w1912-h963-s-no-gm?authuser=0)

Then create a new entry in the dictionary in the constants.py and add the category name, category ID and the tier to it: 

[databricks](https://lh3.googleusercontent.com/pw/AP1GczOFtnp_5zLH2-L8NdxEsQ8DuDGEmyl8nD3UV26yG5WBjGxd6MmxZuS6fgWT-5QFi6cOS4r4ES9wTjUc3ciwsRdFn6kic3XtHEfxFZMCPzN8NmVmwkN2SffGEcynUKk86CGL3WwdPfJCh4DUnkM2Zlvr=w1725-h445-s-no-gm?authuser=0)


## FAQS

1. 
2. 
3. 
4. 


