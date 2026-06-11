# 🚀 AWS End-to-End Cloud Solution Project

## 📌 Project Overview
This project demonstrates the design, architecture, and deployment of a secure and scalable web application on AWS. It implements a full cloud solution using EC2, ALB, S3, CloudFront, IAM, and CI/CD automation with GitHub Actions.

The system follows real-world production architecture principles including high availability, security hardening, and continuous deployment.


## 🎯 Project Objectives
- Design and deploy a scalable web application on AWS
- Implement load balancing using Application Load Balancer (ALB)
- Use CloudFront for content delivery and HTTPS enforcement
- Host backend application on EC2
- Store static assets on S3
- Automate deployment using GitHub Actions CI/CD
- Monitor system performance using CloudWatch
- Apply security best practices using IAM and security groups


## 🏗️ System Architecture

User → CloudFront → Application Load Balancer → EC2 Instance → S3 (Static Assets)


## ☁️ AWS Services Used
- Amazon EC2 – Hosts the web application
- Amazon S3 – Stores static assets (images, CSS, JS)
- Application Load Balancer (ALB) – Distributes traffic across instances
- Amazon CloudFront – CDN for global delivery and HTTPS
- AWS IAM – Access control and permissions
- AWS Certificate Manager (ACM) – SSL/TLS certificate management
- Amazon CloudWatch – Monitoring and logging
- GitHub Actions – CI/CD automation


## 📁 Project Structure
/frontend
├── index.html
├── style.css
└── app.js

/scripts
└── deploy.sh

.github/workflows
└── deploy.yml

---

## ⚙️ Deployment Steps

### 1. AWS Account Setup
- Created AWS Free Tier account
- Configured IAM users with least privilege
- Enabled MFA for root user security


### 2. EC2 Setup
- Launched a t3.micro EC2 instance
- Configured security group:
  - SSH (22)
  - HTTP (80)
  - HTTPS (443)
- Installed web server (Nginx)
- Deployed web application


### 3. S3 Setup
- Created S3 bucket for static assets
- Uploaded images, CSS, and JavaScript files
- Configured access policies


### 4. Load Balancer (ALB)
- Created Target Group and registered EC2 instance
- Configured Application Load Balancer
- Enabled health checks


### 5. CloudFront Setup
- Created CloudFront distribution
- Set ALB as origin
- Enabled HTTPS using ACM certificate
- Configured caching behavior for performance optimization


## 🔐 Security Implementation
- IAM roles follow least privilege principle
- HTTPS enforced using ACM + CloudFront
- EC2 access restricted via security groups
- S3 bucket secured using Origin Access Control (OAC)
- Root account protected with MFA


## 🔄 CI/CD Pipeline

### Workflow:
1. Code pushed to GitHub (main branch)
2. GitHub Actions triggers pipeline
3. SSH into EC2 instance
4. Pull latest code from repository
5. Deploy updated application


## 📊 Monitoring & Logging
- CloudWatch alarms configured:
  - CPU utilization > 80%
  - ALB 5xx errors > 5%
- Logs enabled with 7-day retention policy
- AWS Budget alerts set for cost control

---

## 🧪 Testing & Validation
- EC2 instance health checks passed
- ALB target group shows “healthy”
- CloudFront HTTPS access verified
- Static assets successfully loaded from S3
- End-to-end flow tested:
  Browser → CloudFront → ALB → EC2

---

## 🚀 Live Deployment
- CloudFront URL: https://your-cloudfront-url.com
- Application successfully accessible over HTTPS

---

## 🧑‍💻 Collaboration Tools
- GitHub → Version control and CI/CD
- Trello → Task management and sprint tracking
- Feature branching strategy used:
  - main
  - develop
  - feature/*


## 📌 Challenges Faced
- SSL certificate validation delays in ACM
- ALB health check misconfiguration
- IAM permission issues during setup
- Security group access restrictions


## 📈 Key Learnings
- AWS cloud architecture design
- Load balancing and scaling concepts
- Secure cloud deployment practices
- CI/CD automation using GitHub Actions
- Monitoring and logging with CloudWatch


## 👥 Contributors
- Team Member 1
- Team Member 2
- Team Member 3

## 📌 Future Improvements
- Add Docker containerization
- Use Terraform for Infrastructure as Code
- Implement full auto-scaling
- Add database layer (RDS integration)
