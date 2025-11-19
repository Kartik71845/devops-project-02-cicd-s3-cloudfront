DevOps Project 02 — CI/CD Deployment (GitHub Actions → S3 → CloudFront)
# 🚀 DevOps Project 02 — CI/CD Deployment (GitHub Actions → AWS S3 → CloudFront)

This project demonstrates a **fully automated CI/CD pipeline** where every push to the `main` branch deploys a static website to **Amazon S3** and updates the content on **Amazon CloudFront** using automatic invalidation.

---

## ✅ **Project Overview**
This project showcases:

- GitHub → **CI/CD pipeline**
- AWS S3 → **Static website storage**
- AWS CloudFront → **Global CDN distribution**
- OAC (Origin Access Control) → **Secure access to S3**
- Automatic **cache invalidation** after each deployment

Every push to `main` triggers the pipeline automatically.

---

## 🔧 **Tech Stack Used**
| Tool | Purpose |
|------|---------|
| **GitHub Actions** | CI/CD automation |
| **AWS S3** | Static content hosting |
| **AWS CloudFront** | CDN caching and HTTPS |
| **OAC (Origin Access Control)** | Private S3 access |
| **AWS IAM** | Fine-grained access control |

---

## 📦 **CI/CD Workflow Explanation**

### ✔ Step-by-step pipeline:
1. Checkout GitHub repository  
2. Configure AWS credentials  
3. Install AWS CLI v2  
4. Prepare a clean deploy directory  
5. Upload files to S3 (recursive copy)  
6. Invalidate CloudFront cache  
7. Website updates instantly on global edge locations  

---

## 🗂️ **Repository Structure**


/
├── index.html
├── styles.css
├── script.js
└── .github/workflows/deploy.yml


---

## 🚀 **GitHub Actions Workflow (deploy.yml)**

The workflow:
- Uploads the `deploy/` folder to S3  
- Invalidates CloudFront cache  
- Updates the live website on every push  

Key job steps include:

```yml
aws s3 cp deploy/ s3://$BUCKET --recursive
aws cloudfront create-invalidation --distribution-id $CF_DISTRIBUTION_ID --paths "/*"

🌍 Live CDN URL
https://d1c4y357x2tavv.cloudfront.net/

🔐 Security Highlights

No public S3 bucket

CloudFront accesses S3 via OAC

Only CloudFront can fetch objects

S3 Block Public Access is ON

ACM certificate handled by CloudFront (HTTPS auto-enabled)

🎯 What I learned

How CI/CD works end-to-end

How to deploy to AWS from GitHub Actions

How CloudFront caches and invalidation works

How to secure S3 using OAC

Troubleshooting real-world pipeline issues
