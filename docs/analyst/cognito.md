---
title: Portal User Management
parent: Analyst Engineering Guide
nav_order: 1
last_modified_date: 2025-01-28 12:00
---

# Mediahub Portal User Management Guide

Access to the [Mediahub Portal](https://portal.mediahubww.com/) is managed through **AWS Cognito**. This guide outlines the steps for managing user access, adding users, assigning groups, resetting accounts, and bulk user management.

---

## **Accessing AWS Cognito**
1. Log in to [AWS](https://d-9a673e003c.awsapps.com/start#/).
2. Navigate to [Cognito](https://eu-west-1.console.aws.amazon.com/cognito/v2/idp/user-pools?region=eu-west-1) in the **`eu-west-1` (Ireland)** region.
3. You’ll see the following user pools:
   - **MediahubClientPortalpool-dev**: For the development portal.
   - **MediahubClientPortalpool-prod**: For the production portal.
   - **nbd2_webapi_prod**: For Dev NBD.

   **Use `MediahubClientPortalpool-prod` for adding users to the production portal.**

---

## **Adding a User**
### Steps:
1. In Cognito, under **User Management**, click **Users**.
2. Select **Create User**.
3. Fill in the following details:
   - **Send an email invitation**: Ensure this option is selected.
   - **Email Address**: Enter the user’s email.
   - **Mark email address as verified**: Check this box.
   - Ignore the **Phone Number** field.
   - **Password**: 
     - You can set a password or allow AWS to generate one. If AWS generates the password, it will be emailed to the user, and you won’t have access to it.

---

## **Adding Users to Groups**
After creating a user, assign them to the appropriate group.

### Option 1: Assign via User Profile
1. Navigate to **Users** and search for the user.
2. Click on their username.
3. In the **Group Memberships** section:
   - Click **Add User to Group**.
   - Select the required groups.

### Option 2: Assign via Groups
1. Under **User Management**, click **Groups**.
2. Select the group you want to add users to.
3. Click **Add User to Group** and select the user.

---

## **Resetting User Accounts**
If a user forgets their password and cannot reset it via the portal, it’s often easier to recreate their account.

### Steps:
1. Under **Users**, locate the user.
2. Click their username.
3. In the top-right corner, under **Actions**:
   - Click **Disable User Access**.
   - Then, click **Delete User**.
4. Recreate the user account following the steps in the “Adding a User” section.

---

## **Bulk User Management**
To streamline the process of adding multiple users, use the **CognitoWorker** repository and notebook.

### Steps:
1. Access the [CognitoWorker Repository](https://dbc-341b6afb-df67.cloud.databricks.com/browse/folders/2580965099306873?o=7058903129942627).
2. Open the [Bulk User Creations Notebook](https://dbc-341b6afb-df67.cloud.databricks.com/editor/notebooks/3453432212192136?o=7058903129942627#command/6377198120981527).
3. Prepare your **AWS Credentials**:
   - Log in to [AWS](https://d-9a673e003c.awsapps.com/start#/).
   - Go to **Access Keys** and retrieve your credentials.
4. Add the email addresses to the [Cognito User + Group Add](https://docs.google.com/spreadsheets/d/1lQmrT2EfzLNhm3dcJeVK5mahqN0kfCJKhYhha8lPrK0) Google Sheet under the `AddUsers` tab.
   - Specify the groups for each user. Available groups include:
    ```
   mediahub             testenvironment      hersheys            builderai  
   akzonobel            littlemoons          silversea           westernunion  
   amazondsp            royalcaribbean       hasbro              esprit  
   uber                 activision           valueretail         mediahubmgmt  
   magna                pinterest            premierinn          demo  
   newbalance           celebritycruises     topgolf             newbalanceexternal 
   ```


### Running the Notebook:
1. Follow the prompts in the notebook. When you see:
   ```
   how? Separate variable [S] or all at once [F] (Insert F/S):
   ```
   - Choose **F** to paste all credentials at once or **S** to input them individually.
2. The notebook will:
   - Delete inactive users who haven’t updated their passwords.
   - Create new users based on the email list.
   - Add users to the specified groups.
   - Optionally export passwords if needed.


---

## **Tips**
- Use bulk management for large user additions to save time.
- Always verify group assignments after creating or updating users.
- For sensitive credentials, ensure secure handling and sharing practices.

