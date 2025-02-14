---
title: Getting Started
nav_order: 2
last_modified_date: 2023-11-20 12:00
---

# Getting Started in the Data Team

 
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---


### Databricks

To request Databricks access, contact a Workspace Admin (currently Alvi, Harrison, or Ben). <br> Once acces is shared three simple steps to log in:  
1. Go to the [Databricks Login](https://dbc-341b6afb-df67.cloud.databricks.com/).  
2. Enter your work email (you will recieve an OTP on your email)
3. Enter the verification code.  

{: .note}
For CLI setup instructions, refer to the **Developers Setup** guide.

---

### MySQL Warehouse

The MySQL Warehouse primarily stores data for Akzonobel, Pinterest, and Slack.  

#### Access Details
- **Hostname**: `mlmdata-analytics-cluster.cluster-czxtihb3zgvk.eu-west-1.rds.amazonaws.com`  
- **Username**: `mh.data`  
- **Password**: Contact Engineering Team.  

#### Tools Required
- Mac: Install **Sequel Pro** or **MySQL Workbench**.  
- Windows: Install **MySQL Workbench** and **MySQL drivers** from [MySQL’s official site](https://dev.mysql.com/downloads/connector/).  

{: .important}
For window users should after installing the SQL drivers, PowerBI SQL connections not work then try reinstalling powerbi and restarting.

<br>For Mac users, install MySQL via Homebrew:  
```bash
brew install mysql
```  

{: .note}
You will have `SELECT` and `RUN` permissions. For additional permissions, contact Engineering.


---

### GitHub

Our codebase is hosted on the Mediahub GitHub Organisation: [Mediabrands-MHW-LDN-Github](https://github.com/Mediabrands-MHW-LDN-Github).  

1. Create a GitHub account with your work email. Use a username formatted as:  
   `FirstnameLastname-OpCo` (e.g., AlviChowdhury-MHW).  
2. Request access from an organization owner (Alvi, Harrison, James, or Ben).  
3. Email `githubsupport@interpublic.com` for full access.
4. Email `O365LicenseRequests.SM@corp.ipgnetwork.com` to request and sign the ISR (keep the github support email looped in)
5. You will need the Hyperion billing code - XXXX

---

### AWS

For AWS access, email `kimaya.joshi@interpublic.com`. Permissions are being structured by Alvi and Harrison. Further details will be provided soon.

---

### Power BI

1. Request to be added to the `adtech.analytics@mediahubww.com` distribution email group. Contact Alvi or James.  
   - Manage distribution email group via [this link](https://admin.exchange.microsoft.com/#/).  
2. Access Power BI at [Power BI App](https://app.powerbi.com/).  
3. For contributor access, request a Power BI Pro license from IT: `ITHelpdesk@mbww.com`.  
4. If prompted for Mediahub's Hyperion Code, use: **982940**.

---

### Mediahub Portal

The Mediahub Portal hosts all dashboards and visuals.  

1. Request access from a data team member with AWS access.  
2. You will receive a welcome email with a temporary password.

---

### Egnyte

The D&A shared folder is located at:  
`/Egnyte-mediahubemea/Shared/London/Departments/Analytics`.  

To request access, contact IT (`ITHelpdesk@mbww.com`) and ensure it’s approved by James.

{: .warning}
IPG will be removing Egnyte as a tool in Q1 of 2025 therefore this will become redundant
