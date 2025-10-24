# 🚀 Static Website Hosting on AWS with S3, CloudFront, Route 53, and ACM

This project demonstrates how to host a secure static website on AWS using the following services:

- **Amazon S3** — for static website storage (HTML, CSS, JS, images)
- **Amazon CloudFront** — for CDN caching and HTTPS distribution
- **AWS Certificate Manager (ACM)** — for SSL certificate management
- **Amazon Route 53** — for custom domain DNS routing

---

## 🏗️ Architecture

Users → Route 53 → CloudFront (HTTPS via ACM) → S3 Bucket (static site)

---

## ⚙️ Setup Steps

### 1. Create an S3 Bucket
1. Go to the **S3 Console** → Create a new bucket.
2. Name it with your domain (e.g., `mywebsite.com`).
3. Disable **Block all public access** (since CloudFront will control access).
4. Enable **Static website hosting** and upload your site files (`index.html`, `error.html`, etc.).

### 3. Request an SSL Certificate

Go to **AWS Certificate Manager (ACM)** → Request a public certificate.

Enter your domain (e.g., mywebsite.com, www.mywebsite.com).

Validate via DNS (Route 53 can automate this).

Wait until the status shows “Issued”.

### 4. Create a CloudFront Distribution

Origin domain → Select your S3 bucket (not website endpoint).

Viewer protocol policy → Redirect HTTP to HTTPS.

Add your ACM certificate (must be in us-east-1 for CloudFront).

Cache policy → Use Managed-CachingOptimized.

Save and deploy — note your CloudFront distribution domain name.

### 5. Configure Route 53

In Route 53 → Hosted zones → Select your domain.

Add a **CNAME or ALIAS** record:

Name: @ (root domain)

Alias to: CloudFront distribution domain name.
