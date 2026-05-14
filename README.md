# 🌐 Static Website Hosting with S3 + CloudFront + Route 53

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws)
![S3](https://img.shields.io/badge/S3-Storage-green?logo=amazons3)
![CloudFront](https://img.shields.io/badge/CloudFront-CDN-blue)
![Route53](https://img.shields.io/badge/Route53-DNS-yellow)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📋 Project Overview

This project demonstrates how to host a **fully functional static website** on AWS with global content delivery, HTTPS security, and a custom domain — without managing any servers.

---

## 🚨 Problem

Businesses need fast, reliable, and globally accessible websites without the overhead of managing physical or virtual servers. Traditional hosting is expensive and slow for users in different regions.

---

## ✅ Solution

Built a fully serverless static website hosting architecture using:

| AWS Service | Purpose |
|-------------|---------|
| **S3** | Store and serve website files (HTML, CSS, JS) |
| **CloudFront** | Global CDN for fast content delivery via edge locations |
| **Route 53** | DNS management with custom domain routing |
| **IAM** | Secure bucket policies and access control |

---

## 🏆 Result

- ✅ Globally accessible website with **HTTPS enabled**
- ✅ Fast load times through **CloudFront edge caching**
- ✅ Custom domain configured via **Route 53**
- ✅ Zero server management required

---

## 🏗️ Architecture Diagram

```
User Request
     │
     ▼
Route 53 (DNS)
     │
     ▼
CloudFront (CDN - Edge Location)
     │
     ▼
S3 Bucket (Origin - Website Files)
     │
IAM (Access Control & Bucket Policy)
```

---

## 🛠️ Step-by-Step Setup

### Step 1: Create S3 Bucket
```bash
# Create bucket (replace with your unique name)
aws s3 mb s3://my-static-website-bucket

# Enable static website hosting
aws s3 website s3://my-static-website-bucket \
  --index-document index.html \
  --error-document error.html
```

### Step 2: Upload Website Files
```bash
# Upload your files
aws s3 sync ./website s3://my-static-website-bucket

# Make files publicly readable
aws s3api put-bucket-policy \
  --bucket my-static-website-bucket \
  --policy file://bucket-policy.json
```

### Step 3: Create CloudFront Distribution
- Go to **CloudFront Console** → Create Distribution
- Set **Origin Domain** to your S3 bucket
- Enable **HTTPS** (redirect HTTP to HTTPS)
- Set **Default Root Object** to `index.html`

### Step 4: Configure Route 53
- Create a **Hosted Zone** for your domain
- Add an **A Record** pointing to your CloudFront distribution
- Wait for DNS propagation (up to 48 hours)

---

## 📁 Project Files

```
project1-s3-cloudfront/
├── website/
│   ├── index.html
│   ├── style.css
│   └── script.js
├── bucket-policy.json
└── README.md
```

---

## 💡 Key Learnings

- How S3 static website hosting works
- How CloudFront caches and distributes content globally
- How to configure DNS with Route 53
- How IAM policies control access to S3 buckets

---

## 🔗 Resources

- [AWS S3 Static Website Hosting Docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [CloudFront Developer Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/)
- [Route 53 Documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/)

---

*Built as part of the AWS re/Start Program* ☁️
