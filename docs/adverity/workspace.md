---
title: Onboarding - Workspace
parent: Adverity
nav_order: 2
last_modified_date: 2025-01-20 12:00
---

# Onboarding a New Client

## Workspaces  

To manage data effectively, navigate to the appropriate workspace from the [Datastreams page](https://mullenlowemediahub.datatap.adverity.com/datastreams/list/).  

You can see the available workspaces on the sidebar. 
When creating new workspaces, please ensure the *parent* Workspace is **Mediahub Global | Databricks**.
This will ensure authorisations and destinations can be shared between the child workspaces and the templates generated can be stored in the parent workspace **Mediahub Global | Databricks**.


{: .highlight.title}
> **Value Retail Adverity**
> 
> Uses a separate Adverity instance. Access it [here](https://valueretail.datatap.adverity.com/).  

---

### Guidelines for Workspaces  

#### 1. Handling New Clients or Expansions
When onboarding a new client or expanding services for an existing client:  
- **Create a New Workspace** to ensure clear separation between clients.  
- For **new clients**, set the **parent workspace** to `Mediahub Global | Databricks`

#### 2. Destinations and Authorisations
- When creating **new destinations** or **new authorisations**, configure them under the `Mediahub Global | Databricks` workspace.  
- This allows sharing across child workspaces.  
- If a client-specific configuration is required, use the client’s workspace instead.  

{: .note-title}
> Current State
>  
> The **Global Databricks workspace** contains multiple clients.  
> Value Retail uses its own Adverity instance which the client owns.  

