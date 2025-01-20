---
title: Getting Started
nav_order: 1
---

# Getting Started in the Data Team

## Table of Contents
- [Getting Started in the Data Team](#getting-started-in-the-data-team)
  - [Table of Contents](#table-of-contents)
  - [What You Can Get Access To](#what-you-can-get-access-to)
    - [Databricks](#databricks)
    - [MySQL Warehouse](#mysql-warehouse)
      - [Access Details:](#access-details)
      - [Tools Required:](#tools-required)
    - [GitHub](#github)
      - [Steps to Join:](#steps-to-join)
    - [AWS](#aws)
    - [Power BI](#power-bi)
      - [Steps to Access Power BI:](#steps-to-access-power-bi)
    - [Mediahub Portal](#mediahub-portal)
      - [Steps to Access:](#steps-to-access)
    - [Egnyte](#egnyte)
    - [Connecting Databricks to Power BI](#connecting-databricks-to-power-bi)
      - [Within Databricks:](#within-databricks)
      - [Within Power BI:](#within-power-bi)

---

## What You Can Get Access To  

Below are the various platforms the D&A team has access to, and how you can gain access:

---

### Databricks

To request Databricks access, contact a Workspace Admin (currently Alvi, Harrison, or Ben). Follow these steps to log in:  
1. Visit [Databricks Login](https://dbc-341b6afb-df67.cloud.databricks.com/).  
2. Enter your work email, verify your login, and enter the verification code.  

_For CLI setup instructions, refer to the **mac-setup.md** guide._

---

### MySQL Warehouse

The MySQL Warehouse primarily stores data for Akzonobel, Pinterest, and Slack.  

#### Access Details:
- **Hostname**: `mlmdata-analytics-cluster.cluster-czxtihb3zgvk.eu-west-1.rds.amazonaws.com`  
- **Username**: `mh.data`  
- **Password**: Contact Alvi.  

#### Tools Required:
- Mac: Install **Sequel Pro** or **MySQL Workbench**.  
- Windows: Install MySQL drivers from [MySQL’s official site](https://dev.mysql.com/downloads/connector/).  

For Mac users, install MySQL via Homebrew:  
```bash
brew install mysql
```  

You will have `SELECT` and `RUN` permissions. For additional permissions, contact Alvi.

---

### GitHub

Our codebase is hosted on the Mediahub GitHub Organisation: [Mediahub GitHub](https://github.com/Mediabrands-MHW-LDN-Github).  

#### Steps to Join:
1. Create a GitHub account with your work email. Use a username formatted as:  
   `FirstnameLastname-OpCo` (e.g., AlviChowdhury-MHW).  
2. Request access from an organization owner (Alvi, Harrison, James, or Ben).  
3. Email `githubsupport@interpublic.com` for full access.

---

### AWS

For AWS access, email `kimaya.joshi@interpublic.com`. Permissions are being structured by Alvi and Harrison. Further details will be provided soon.

---

### Power BI

#### Steps to Access Power BI:
1. Request to be added to the `adtech.analytics@mediahubww.com` distribution email group. Contact Alvi or James.  
   - Manage distribution email group via [this link](https://admin.exchange.microsoft.com/#/).  
2. Access Power BI at [Power BI App](https://app.powerbi.com/).  
3. For contributor access, request a Power BI Pro license from IT: `ITHelpdesk@mbww.com`.  
4. If prompted for Mediahub's Hyperion Code, use: **982940**.

---

### Mediahub Portal

The Mediahub Portal hosts all dashboards and visuals.  

#### Steps to Access:
1. Request access from a data team member with AWS access.  
2. You will receive a welcome email with a temporary password.

---

### Egnyte

The D&A shared folder is located at:  
`/Egnyte-mediahubemea/Shared/London/Departments/Analytics`.  

To request access, contact IT (`ITHelpdesk@mbww.com`) and ensure it’s approved by James.

_IPG will be removing Egnyte as a tool in Q1 of 2025 therefore this will become redundant_

---

### Connecting Databricks to Power BI

To establish a connection between Power BI and Databricks, follow these steps:

#### Within Databricks:
1. Log into Databricks: [Databricks Login](https://dbc-341b6afb-df67.cloud.databricks.com/).  
2. Click your account name in the top-right corner and go to **Settings**.  
3. Under the **User** subheader, select **Developer**.  
4. In the **Access Tokens** section, click **Manage**.  
5. Generate a new token and optionally provide a description.  
6. **Important**: Copy the token immediately and store it securely, as it will not be displayed again.

#### Within Power BI:
1. Click **Get Data** or navigate to **File > Get Data**.  
2. Search for **Databricks** and select the **Azure Databricks** connector.  
3. Click **Connect**.  
4. Enter the required details for the compute cluster being used:  
   - **Host**: `dbc-341b6afb-df67.cloud.databricks.com`  
   - **HTTP Path**: `sql/protocolv1/o/7058903129942627/0209-113722-jcsrnoj7`  
   *(As of January 2025, the default cluster is the **DataOps Shared Compute Cluster**.)*  
5. Choose a **Data Connectivity mode**:  
   - **Direct**: Enables live refreshes.  
   - **Import**: Requires scheduled refreshes.  
6. Click **OK**.  
7. For the **Authentication Method**, select **Personal Access Token** and enter the token you generated in Databricks.  
8. Click **Connect** to establish the connection.

---
