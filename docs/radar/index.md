---
title: RADAR
layout: default
nav_order: 8
last_modified_date: 2025-01-20 12:00
---

# RADAR

## Overview

RADAR aims to unify online and offline media data to enable greater and granular analysis of media activity. 


## MediaPlan Template

This starts with the MediaPlan Template which is standardised. Example file here. 

Work with Roland and the Account Director for the client to help inform the template and make changes to this. 


## General Workflow

```mermaid
graph LR;
    accTitle: Very High Level Overview
    accDescr: RADAR Overview
    A[Standardised MediaPlan Template]-->B[RADAR Client Portal];
    B-->C[Canonical Check];
    C-->D[Bronze MediaPlan Table];
```

## Technical Workflow

What  happens in databricks after a file is uploaded into the `uploads` folder. 

```mermaid
graph TD;

MP[MediaPlan Uploaded to the **uploads** folder] --> T1[Triggers the **TRIGGER** Worflow]
T1 --> Task1[The Trigger Notebook is Run]
Task1 --> Task2[Trigger Notebook Generates a Job within the **RUNNER** Workflow]
Task2 --> Task2A[MediaPlan is run through the Main MediaPlan Notebook]
Task2A --> Task2B[MediaPlan is categorised into a _Failed_ or _Successful_ Plan]
Task2B --> Task2C[MediaPlan is shifted to a _Sucess_ or _Failed_ Folder]
Task2A --> Task3A[Next Stage of **TRIGGER** Workflow. This is the Update Notebook]
Task3A --> Task3B[Update MediaPlan Notebook is run. Ensuring Latest MediaPlan are active]
Task3B --> Task4[Next stage of **TRIGGER** Notebook is run. This is where the Gold Table is gernally defined]

```

## Testing