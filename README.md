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

### 2. Request an SSL Certificate

1. Go to **AWS Certificate Manager (ACM)** → Request a public certificate.

2. Enter your domain (e.g., mywebsite.com, www.mywebsite.com).

3. Validate via DNS (Route 53 can automate this).

4. Wait until the status shows “Issued”.

### 3. Create a CloudFront Distribution

1. Origin domain → Select your S3 bucket (not website endpoint).

2. Viewer protocol policy → Redirect HTTP to HTTPS.

3. Add your ACM certificate (must be in us-east-1 for CloudFront).

4. Cache policy → Use Managed-CachingOptimized.

5. Save and deploy — note your CloudFront distribution domain name.

### 5. Configure Route 53

1. In Route 53 → Hosted zones → Select your domain.

2. Add a **CNAME or ALIAS** record:

3. Name: @ (root domain)

4. Alias to: CloudFront distribution domain name.

<img width="1369" height="627" alt="Screenshot (700)" src="https://github.com/user-attachments/assets/70159409-4f5c-4412-aaf0-8fecaa5d74fa" />
