# TechCrush-AWS-StaticWeb 
This repository contains the source code for a basic static website built with HTML and inline-CSS, and details the steps taken to deploy it using **Visual Studio Code (VS Code)** and **AWS Simple Storage Service (S3)**.

## Deployment Steps Summary

1.  **Local Development:** Created static files (`index.html`).
2.  **Version Control (VS Code/Git):** Initialized a local Git repository, committed files, and pushed them to a remote repository.
3.  **Cloud Deployment (AWS S3):** Created and configured an S3 bucket for static website hosting.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 🛠️ Local Setup and Version Control (VS Code & Git)

### 1. Project Initialization

* A local folder (`TechCrush-AWS-StaticWeb`) was created and opened in VS Code.
* The index.html file was created in the root directory.

### 2. Git Initialization and Commit

**Process:**
1.  Opened **Source Control** (Ctrl+Shift+G) in VS Code.
2.  Selected **Initialize Repository**.
3.  Staged all files and committed with a message: `Added Static Web To Main`.

### 3. Connecting to Remote Repository (Cloning/Publishing)

**Process:**
1.  A corresponding empty repository was created on GitHub.
2.  In VS Code Source Control, used the `...` menu -> **Push** -> **Add Remote...**.
3.  Added the remote URL and pushed the changes to the `origin` remote.

**Common Errors & Troubleshooting:**

| Error | Description | Resolution |
| :--- | :--- | :--- |
| **Authentication Failure** | `Authentication failed for 'https://github.com/...'` during push. | Ensure you are using a **Personal Access Token (PAT)** instead of your password for HTTPS clones, or set up SSH keys for SSH clones. |
| **No Remote Set** | `fatal: The current branch master has no upstream branch.` | Use the command `git push --set-upstream origin main` (or `master`) to explicitly link your local branch to the remote one. |

---



## ☁️ AWS S3 Static Website Hosting

### 1. S3 Bucket Creation

**Configuration Details:**
* **Bucket Name:** `YOUR_BUCKET_NAME` (Must be globally unique)
* **Region:** `YOUR_REGION`
* **Block Public Access:** **DISABLED** (Unchecked) to allow public website access.

### 2. Static Website Hosting Configuration

**Process:**
1.  Navigate to the **Properties** tab of the bucket.
2.  Enabled **Static website hosting**.
3.  Set **Index document** to `index.html`.
4.  **Endpoint URL:** `http://YOUR_BUCKET_NAME.s3-website-YOUR_REGION.amazonaws.com`

### 3. File Upload

**Process:**
* All project files (`index.html`, `styles.css`, `script.js`, etc.) were uploaded to the root of the S3 bucket.

### 4. Public Bucket Policy

The following Bucket Policy was applied under the **Permissions** tab to allow public **read** access (`s3:GetObject`) to all objects in the bucket.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}
