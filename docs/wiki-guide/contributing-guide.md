---
title: Contributing
parent: Wiki Guide
nav_order: 1
last_modified_date: 2025-01-27 12:00
---

# Contributing to the Wiki

This guide is for beginners looking to contribute to the Mediahub GitHub repository. Whether you're editing directly on GitHub or using an Integrated Development Environment (IDE) like VSCode, follow these steps to ensure a smooth contribution process.

---

## Access

Before you can contribute, you must have the necessary permissions to access the Mediahub GitHub repository: [Mediabrands-MHW-LDN-Github](https://github.com/Mediabrands-MHW-LDN-Github)

1. **Get Access to Github**
   
   1. Create a GitHub account with your work email. Use a username formatted as:  
   `FirstnameLastname-OpCo` (e.g., AlviChowdhury-MHW).  
   2. Request access from an organisation owner (Harrison, James, or Ben).  
   3. Email `githubsupport@interpublic.com` for them to approve access.

2. **Check Your Access**  
   - If you see an error like "Permission Denied" or cannot create branches, you probably lack write access.  

3. **Request Access**  
   - Contact one of the GitHub Admins (Harrison, James, Ben).  
   - Ask to be added to the **_Analyst_** team within the organization.  

---

## How to Contribute

There are two main ways to contribute:  
1. Using the **GitHub Web GUI** for smaller or quick edits.  
2. Using an **IDE like VSCode** for more complex changes.  

### **Option 1: Contributing via GitHub Web GUI**

The simplest way to edit or add files.  

1. **Create a Branch**  
   - Open the repository in GitHub.  
   - Use the "Branch" dropdown in the top-left corner.  
   - Name your branch descriptively (e.g., `alvi/update-contributing-guide`).  

2. **Edit Files**  
   - Navigate to the file you want to edit (e.g., `docs/wiki-guide/contributing.md`).  
   - Click the pencil icon in the top-right corner to edit the file.  

3. **Commit Your Changes**  
   - Add a **commit message** (e.g., `Update contributing guide for new users`).  
   - Select “Commit directly to this branch.”  

---

### **Option 2: Contributing via an IDE (e.g., VSCode)**

For more complex changes or working on multiple files.  

#### **Prerequisites**  
- Install [Git](https://git-scm.com/) and [VSCode](https://code.visualstudio.com/).  
- Authenticate with GitHub using SSH or HTTPS.  

#### **Steps**  

1. **Clone the Repository**  
   - Open your terminal:  
     ```bash
     git clone https://github.com/Mediabrands-MHW-LDN-Github/Wiki.git
     ```  
   - Navigate to the project folder:  
     ```bash
     cd Wiki
     ```  

2. **Create a New Branch**  
   - Create and switch to a new branch:  
     ```bash
     git checkout -b alvi/update-contributing-guide
     ```  

3. **Make Edits**  
   - Open the project in VSCode.  
   - Edit the relevant file(s).  

4. **Preview Changes**  
   - Use the Markdown Preview in VSCode:  
     - Right-click your file and select **Markdown Preview Enhanced**.  

5. **(Optional) Local Preview Using Jekyll**  
   - For advanced users who want to see how the changes render on the site:  
     - Install [Ruby](https://www.ruby-lang.org/en/documentation/installation/).  
     - Install Jekyll:  
       ```bash
       gem install jekyll bundler
       ```  
     - Run the local server:  
       ```bash
       bundle install
       bundle exec jekyll serve
       ```  
     - View your changes at `http://127.0.0.1:4000/`.  

6. **Commit Your Changes**  
   - Stage and commit your edits:  
     ```bash
     git add .
     git commit -m "Update contributing guide for clarity"
     ```  

7. **Push Your Changes**  
   - Push your branch to the remote repository:  
     ```bash
     git push origin alvi/update-contributing-guide
     ```  

---

### Create a Pull Request  

After pushing your changes, you need to merge them into the `main` branch.  

1. **Open a Pull Request**  
   - Go to the **Pull Requests** tab in GitHub.  
   - Select "New Pull Request" and compare your branch with `main`.  

2. **Add Details**  
   - Write a descriptive title (e.g., `Update contributing guide`).  
   - Add a summary of your changes.  

3. **Submit and Respond to Feedback**  
   - Submit your pull request for review.  
   - Be open to feedback from reviewers and make necessary changes.  

---

## Best Practices  

1. **Use Descriptive Branch Names**  
   - Include your name and purpose, e.g., `alvi/fix-typo-readme`.  

2. **Write Clear Commit Messages**  
   - Use present tense: e.g., `Add contributing guide`.  

3. **Test Your Changes**  
   - Preview markdown locally or test scripts before committing.  

4. **Follow Style Guidelines**  
   - Check for naming conventions and formatting standards in the repository.  

5. **Communicate Clearly**  
   - Add meaningful comments to your pull request.  
   - Respond promptly to feedback.  
