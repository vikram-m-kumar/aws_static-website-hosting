# Secure Static Website Hosting on AWS with CI/CD Pipeline

## 📖 Project Overview
This project demonstrates a serverless architecture for hosting a static website on AWS. It leverages **Amazon S3** for storage, **CloudFront** for secure global content delivery, and **Route 53** for DNS management. 

To automate the deployment workflow, I implemented a CI/CD pipeline using **AWS CodePipeline**. Any commit made to the connected GitHub repository automatically triggers a deployment, updating the live website without manual intervention.


## 🛠 Tech Stack
* **Cloud Provider:** Amazon Web Services (AWS)
* **Storage:** Amazon S3 (Simple Storage Service)
* **CDN:** Amazon CloudFront
* **DNS:** Amazon Route 53
* **Security:** AWS Certificate Manager (ACM), Bucket Policies, Origin Access Identity (OAI)
* **CI/CD:** AWS CodePipeline
* **Version Control:** Git & GitHub

## 🏗 Architecture & Features
* [cite_start]**High Availability & Performance:** Uses CloudFront to cache content at edge locations globally[cite: 1254].
* [cite_start]**Security:** * **HTTPS Only:** SSL/TLS certificate provisioned via ACM[cite: 1341].
    * [cite_start]**Private Origin:** S3 bucket public access is strictly blocked[cite: 1117]. [cite_start]Access is only allowed via CloudFront using an Origin Access Identity (OAI)[cite: 1277].
* [cite_start]**Automation:** AWS CodePipeline monitors the GitHub repository (main branch) and deploys changes to S3 automatically[cite: 1571].

## 🚀 Implementation Steps

### 1. Domain & Storage Setup
* [cite_start]**Registered Domain:** Configured a custom domain (e.g., `static-website-hosting.org`) using **Route 53**[cite: 1038].
* **S3 Bucket:** Created a bucket with a name matching the domain. [cite_start]Enabled *Static Website Hosting* and set `index.html` as the default document[cite: 1095, 1189].
* [cite_start]**Access Control:** Blocked all public access to the bucket to ensure security[cite: 1119].

### 2. Security & Content Delivery (CloudFront)
* [cite_start]**Distribution:** Created a CloudFront distribution pointing to the S3 bucket's website endpoint[cite: 1264].
* [cite_start]**OAI Configuration:** Generated an Origin Access Identity (OAI) and updated the S3 Bucket Policy to allow access *only* from this OAI[cite: 1277, 1281].
* [cite_start]**HTTPS:** Configured the Viewer Protocol Policy to "Redirect HTTP to HTTPS"[cite: 1301].
* [cite_start]**SSL Certificate:** Requested a public certificate in `us-east-1` via **ACM** and validated it using DNS CNAME records in Route 53[cite: 1348, 1374].

### 3. DNS Configuration
* [cite_start]Created **A Records (Alias)** in Route 53 to route traffic from the custom domain to the CloudFront distribution domain name[cite: 1486].

### 4. CI/CD Pipeline Configuration
* **Source Stage:** Connected AWS CodePipeline to this GitHub repository.
* [cite_start]**Deploy Stage:** Configured the pipeline to extract and deploy files directly to the S3 bucket[cite: 1664].
* [cite_start]**Build/Test:** Skipped build stages as this is a purely static site[cite: 1658].

## ⚙️ How to Deploy Updates
1.  Clone the repository:
    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    ```
2.  Make changes to `index.html` or `style.css`.
3.  Push changes to GitHub:
    ```bash
    git add .
    git commit -m "Update homepage content"
    git push origin main
    ```
4.  **Result:** CodePipeline detects the commit, fetches the changes, and updates the S3 bucket. The website updates automatically within minutes.

## ⚠️ Troubleshooting & Lessons Learned
* **Pipeline Directory Structure:** Initially, files were in a subfolder (`website_files/`), which caused the S3 deployment to nest files incorrectly. [cite_start]The solution was to move all website files to the **root** of the repository so the pipeline deploys them correctly to the root of the S3 bucket[cite: 993, 995].
* **Caching:** CloudFront aggressively caches content. [cite_start]If updates aren't visible immediately, an invalidation (`/*`) may be required, or simply wait for the TTL to expire[cite: 989].

## 📜 License
This project is open-source and available under the MIT License.
