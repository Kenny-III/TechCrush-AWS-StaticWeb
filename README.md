# TechCrush-AWS-StaticWeb 
This repository contains the source code for a basic static website built with HTML and inline-CSS, and details the steps taken to deploy it using **Visual Studio Code (VS Code)** and **AWS Simple Storage Service (S3)**.

![TechCrush Logo Image](Techcrush-Image.png)

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

**Error Encountered & How I Resolved it:**

| Error | Description | Resolution |
| :--- | :--- | :--- |
| **<Code>AccessDenied </Code> <Message>Access Denied </Message>** | The browser displays an XML page with this error when attempting to navigate to the S3 Website Endpoint URL `https://techcrush-s3-staticweb.s3.eu-north-1.amazonaws.com/index.html`. | Applying Bucket Policy: Ensured the Bucket Policy is present in the Permissions tab and correctly grants Effect": 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::techcrush-s3-staticweb/*"
        }
    ]
}. |



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



## ☁️ AWS S3 Static Website Hosting

### 1. S3 Bucket Creation

**Configuration Details:**
* **Bucket Name:** `techcrush-s3-staticweb`
* **Region:** `eu-north-1`
* **Block Public Access:** **DISABLED** (Unchecked) to allow public website access.

### 2. Static Website Hosting Configuration

**Process:**
1.  Navigate to the **Properties** tab of the bucket.
2.  Enabled **Static website hosting**.
3.  Set **Index document** to `index.html`.
4.  **Endpoint URL:** `(https://techcrush-s3-staticweb.s3.eu-north-1.amazonaws.com/index.html)`

### 3. File Upload

**Process:**
* The Project file (`index.html`) were uploaded to the root of the S3 bucket.

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
            "Resource": "arn:aws:s3:::techcrush-s3-staticweb/*"
        }
    ]
}
