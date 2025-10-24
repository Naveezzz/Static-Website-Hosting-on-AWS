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

### 2. Configure the Bucket Policy
Attach the following **bucket policy** (replace `YOUR_BUCKET_NAME` and `YOUR_CLOUDFRONT_ID`):

```json
{
  "Version": "2012-10-17",
  "Id": "PolicyForCloudFrontPrivateContent",
  "Statement": [
    {
      "Sid": "GrantCloudFrontAccess",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::YOUR_AWS_ACCOUNT_ID:distribution/YOUR_CLOUDFRONT_ID"
        }
      }
    }
  ]
}
