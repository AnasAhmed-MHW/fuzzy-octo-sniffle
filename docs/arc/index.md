---
title: ARC
layout: default
nav_order: 9
last_modified_date: 2025-04-29 12:00
---

# ARC

## Overview

ARC (Attention-based Reach & Context) uses Lumen attention data to drive contextual targeting strategies across DSPs, enhancing performance through attention-optimized domain lists. The ARC repository operates only on the **DataOps Shared Compute Cluster**, where required API credentials and secrets are securely stored.

---

## Supported DSPs

- **Tradedesk** (TDD)
- **Yahoo DSP**

ARC supports campaign setup, bidlist and whitelist management, and performance tracking across both platforms.

---

## General Campaign Setup Workflow

```mermaid
graph TD;
    A[Define Campaign in Dictionary] --> B[Choose Action: test / create / refresh / attach];
    B --> C[Run Notebook - TDD or Yahoo];
    C --> D[Bidlist and Whitelist Created / Attached];
    D --> E[Campaign Updated in DSP];

