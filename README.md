# 🚀 Learn React with AWS CI/CD Pipeline

---

## 💡 Introduction

Hi there. This project is my first ever cloud project. This project demonstrates a complete **production-ready CI/CD pipeline** built on AWS, designed to automate every step from code commit to global content delivery. I created a static website using react (Learn React). This project is my first practical skill that i applied after few weeks diving in cloud technologies theories. The key highlight of this project is the CI/CD pipeline that i created to help developers smoothly deliver updates, testing and deploy automatically.

---

## 📸 Project Overview

![image alt](https://github.com/mrzaazhar/React-App-with-Full-CI-CD-Pipeline-on-AWS-GitHub-CodePipeline-S3/blob/2e4b6db534fd726619d5aec03ca25ea87fba1026/Screenshot%202026-02-25%20093058.png)

*Learn React Interface: d22w6jdd9ptive.cloudfront.net*

---

## 🎯 What Makes This Project Special?

- 🔄 **Fully Automated CI/CD** - Zero manual deployment steps
- ☁️ **Cloud-Native Architecture** - Built entirely on AWS
- ⚡ **Lightning-Fast Delivery** - Global CDN via CloudFront
- 🔒 **Infrastructure as Code Ready** - Scalable and maintainable

---

## 🛠️ Tech Stack

### Frontend
![React](https://img.shields.io/badge/React-18.0-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

### Cloud Infrastructure (AWS)
![AWS CodePipeline](https://img.shields.io/badge/AWS-CodePipeline-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![AWS CodeBuild](https://img.shields.io/badge/AWS-CodeBuild-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![AWS S3](https://img.shields.io/badge/AWS-S3-569A31?style=for-the-badge&logo=amazonaws&logoColor=white)
![AWS CloudFront](https://img.shields.io/badge/AWS-CloudFront-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)

### Source Control
![GitHub](https://img.shields.io/badge/GitHub-Integration-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 🏗️ Architecture Overview

![image alt](https://github.com/mrzaazhar/React-App-with-Full-CI-CD-Pipeline-on-AWS-GitHub-CodePipeline-S3/blob/d9160f36dd5a1d8e4957c0cb26a57a9a1e5c3b85/Screenshot%202026-02-23%20162951.png)

*Pipeline flow: GitHub → CodePipeline → CodeBuild → S3 → CloudFront*

### Pipeline Flow

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐     ┌──────────────┐     ┌──────────────┐
│   GitHub    │────▶│  AWS CodePipeline│────▶│  AWS CodeBuild  │────▶│   AWS S3     │────▶│  CloudFront  │
│   (Push)    │     │   (Orchestration)│     │   (Build & Test)│     │  (Storage)   │     │    (CDN)     │
└─────────────┘     └──────────────────┘     └─────────────────┘     └──────────────┘     └──────────────┘
                      Trigger on Commit         Build Production       Deploy Static        Global Delivery
                                               Bundle                 Files
```
---

## 🔥 How It Works

### 1️⃣ **Developer Pushes Code**
```bash
git add .
git commit -m "feature: amazing new feature"
git push origin main
```

### 2️⃣ **GitHub Triggers AWS CodePipeline**
- CodePipeline automatically detects the push
- Initiates the deployment process

### 3️⃣ **AWS CodeBuild Builds & Tests**
- Installs dependencies
- Runs production build
- Executes test suite
- Creates optimized static assets

![image alt](https://github.com/mrzaazhar/React-App-with-Full-CI-CD-Pipeline-on-AWS-GitHub-CodePipeline-S3/blob/143a98bce63d1ac29cbf587217cf8f41cbc6cf9f/Screenshot%202026-02-24%20105235.png)

*Screenshot of AWS CodeBuild console showing build logs and success*

### 4️⃣ **Deploy to AWS S3**
- Optimized build artifacts are uploaded to S3
- Static hosting enabled for fast access
- Version control for rollback capability

![image alt](https://github.com/mrzaazhar/React-App-with-Full-CI-CD-Pipeline-on-AWS-GitHub-CodePipeline-S3/blob/59d57cd02796b670711aba260bc63d1ca6f7b113/Screenshot%202026-02-24%20105337.png)

*Screenshot of S3 bucket showing the deployed React app files*

### 5️⃣ **CloudFront Delivers Globally**
- Content cached at edge locations worldwide
- Reduced latency for global users
- Faster content delivery network (CDN)

![image alt](https://github.com/mrzaazhar/React-App-with-Full-CI-CD-Pipeline-on-AWS-GitHub-CodePipeline-S3/blob/882bd64b0aada17a709a932f5862f55829819611/Screenshot%202026-02-24%20105608.png)

*Open Link: d22w6jdd9ptive.cloudfront.net*

---

## ✨ Key Features

### 🚀 **Automated Deployment**
- **Zero Downtime**: Seamless deployments with no service interruption
- **Rollback Ready**: Quick revert to previous versions
- **Instant Updates**: Changes live in minutes, not hours

### 🌍 **Global Performance**
- **Edge Caching**: Content served from 400+ edge locations
- **Compression**: Optimized file sizes for faster loading

### 🔒 **Security & Reliability**
- **CI/CD Best Practices**: Automated testing before deployment
- **Version Control**: Full traceability of all deployments

### 📊 **Monitoring & Logs**
- **Build Logs**: Detailed CodeBuild logs for debugging
- **Pipeline Status**: Real-time deployment tracking
- **Error Alerts**: Notifications on failures

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ installed
- AWS Account with appropriate permissions
- GitHub account

### Local Development

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO

# Install dependencies
npm install

# Start development server
npm start

# Build for production
npm run build

# Run tests
npm test
```

---

## 📦 Deployment Pipeline Configuration

### AWS CodePipeline
The pipeline is configured with these stages:

| Stage | Service | Purpose |
|-------|---------|---------|
| Source | GitHub | Triggers on push to main branch |
| Build | CodeBuild | Compiles, tests, and builds React app |
| Deploy | S3 + CloudFront | Deploys static files and invalidates cache |

### CodeBuild Buildspec
```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 18
  pre_build:
    commands:
      - npm install
  build:
    commands:
      - npm run build
      - npm test
  post_build:
    commands:
      - aws s3 sync ./build s3://YOUR_BUCKET_NAME --delete
      - aws cloudfront create-invalidation --distribution-id YOUR_DISTRIBUTION_ID --paths "/*"
```
## 📧 Contact

- **Developer**: Mirza
- **Email**: mirzaazhar5963@gmail.com

---
