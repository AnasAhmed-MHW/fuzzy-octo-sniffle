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

