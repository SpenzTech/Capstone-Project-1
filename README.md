# 🚀 AWS End-to-End Cloud Solution Project

> **Capstone Project — AWS Free Tier | Intern Cohort**
> Designed, architected, and deployed a secure, scalable web application on AWS using CloudFront, ALB, EC2, S3, IAM, ACM, and GitHub Actions CI/CD automation.

---

## 📌 Project Overview

This project demonstrates the design, architecture, and deployment of a production-grade web application on AWS. It implements a full cloud solution following real-world principles including high availability, security hardening, and continuous deployment.

The system architecture follows:
```
User → CloudFront (HTTPS) → Application Load Balancer → EC2 (Nginx) → S3 (Static Assets)
```

---

## 🎯 Project Objectives

- Design and deploy a scalable web application on AWS
- Implement load balancing using Application Load Balancer (ALB)
- Use CloudFront for global content delivery and HTTPS enforcement
- Host the backend web application on EC2
- Store and serve static assets via S3
- Automate deployment using GitHub Actions CI/CD
- Monitor system performance using CloudWatch
- Apply security best practices using IAM least-privilege and security groups

---

## 🏗️ System Architecture

```
Browser (HTTPS)
      │
      ▼
Amazon CloudFront  ◄──── ACM (SSL/TLS Certificate)
      │
      ▼
Application Load Balancer (ALB)  ◄──── IAM (Least Privilege)
      │
      ▼
EC2 Instance (t3.micro) — Nginx Web Server
      │
      ▼
Amazon S3 (Static Assets: Images, CSS, JS)

──────────────────────────────────────
CI/CD Pipeline (separate flow):

GitHub (push to main)
      │
      ▼
GitHub Actions (deploy.yml)
      │
      ▼
SSH into EC2 → git pull → reload Nginx
```

---

## ☁️ AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon EC2** | Hosts the web application (t3.micro, Amazon Linux 2023) |
| **Amazon S3** | Stores static assets (images, CSS, JS) |
| **Application Load Balancer (ALB)** | Distributes traffic across instances |
| **Amazon CloudFront** | CDN for global content delivery and HTTPS |
| **AWS IAM** | Access control and least-privilege permissions |
| **AWS Certificate Manager (ACM)** | SSL/TLS certificate management |
| **Amazon CloudWatch** | Monitoring, logging, and alarms |
| **GitHub Actions** | CI/CD automation pipeline |

---

## 📁 Project Structure

```
/
├── index.html
├── beyondTheClassroom.html
├── learning.html
├── news.html
├── ourSchool.html
├── css/
│   ├── styles.css
│   └── normalize.css
├── js/
│   └── main.js
├── images/
│   └── (all static image assets)
├── .github/
│   └── workflows/
│       └── deploy.yml
└── README.md
```

---

## ⚙️ Deployment Steps

### Phase 1 — AWS Account Setup
- Created AWS Free Tier account
- Configured IAM users with least-privilege permissions
- Enabled MFA for root user security
- Installed and configured AWS CLI with named profiles

### Phase 2 — EC2 Setup
- Launched a **t3.micro** EC2 instance (Amazon Linux 2023)
- Configured security group:
  - SSH (port 22)
  - HTTP (port 80)
  - HTTPS (port 443)
- Installed Nginx web server
- Deployed web application to `/var/www/html`

### Phase 3 — S3 Setup
- Created S3 bucket for static assets
- Uploaded images, CSS, and JavaScript files
- Configured public access settings
- Applied S3 bucket policy for CloudFront Origin Access Control (OAC)

### Phase 4 — Load Balancer (ALB)
- Created Target Group and registered EC2 instance
- Configured Application Load Balancer
- Enabled health checks
- Configured listener rules for HTTP → HTTPS redirect

### Phase 5 — CloudFront Setup
- Created CloudFront distribution with ALB as origin
- Attached ACM certificate to enforce HTTPS
- Configured caching behaviors for static assets and performance optimization
- Restricted EC2 security groups to only accept traffic from CloudFront

### Phase 6 — CI/CD Pipeline (GitHub Actions)
- Created `.github/workflows/deploy.yml`
- Configured GitHub Secrets:
  - `EC2_HOST` — public IP of EC2 instance
  - `EC2_USERNAME` — `ec2-user`
  - `EC2_SSH_KEY` — RSA private key for SSH access
- Pipeline triggers on every push to `main` branch
- Workflow: SSH into EC2 → `git pull origin main` → `sudo systemctl reload nginx`

---

## 🔒 Security Implementation

| Control | Implementation |
|---|---|
| IAM roles | Least-privilege principle applied to all services |
| HTTPS | Enforced via CloudFront's built-in SSL on `.cloudfront.net` domain (ACM cert requested but did not validate within project timeframe) |
| EC2 access | Restricted via security groups (no open inbound except 80/443/22) |
| S3 access | Secured using CloudFront Origin Access Control (OAC) |
| Root account | Protected with MFA |
| SSH key | Stored as GitHub Secret — never committed to repo |

---

## 🔄 CI/CD Pipeline

**Workflow** (`.github/workflows/deploy.yml`):

1. Code pushed to `main` branch on GitHub
2. GitHub Actions triggers the workflow automatically
3. Runner SSHs into EC2 instance using stored secrets
4. Pulls latest code from the repository
5. Reloads Nginx to serve the updated application

Every push to `main` deploys to production with zero manual steps.

---

## 📊 Monitoring & Logging

- **CloudWatch Alarms** configured for:
  - CPU utilization > 80%
  - ALB 5xx errors > 5%
- **CloudWatch Logs** enabled with 7-day retention policy
- **AWS Budget Alerts** set for Free Tier cost control

---

## ✅ Testing & Validation

| Test | Result |
|---|---|
| EC2 instance health checks | ✅ Passed |
| ALB target group status | ✅ Healthy |
| CloudFront HTTPS access | ✅ Verified |
| Static assets loaded from S3 | ✅ Confirmed |
| End-to-end flow | ✅ Browser → CloudFront → ALB → EC2 |
| GitHub Actions pipeline | ✅ Deploys on push to main |

---

## 🌐 Live Deployment

- **CloudFront URL:** `https://your-cloudfront-url.cloudfront.net`
- Application accessible over HTTPS globally via CloudFront CDN

---

## 🤝 Collaboration Tools

| Tool | Purpose |
|---|---|
| **GitHub** | Version control, CI/CD, pull requests, peer code review |
| **Trello** | Agile task management and sprint tracking |

**Branching strategy:**
- `main` — production branch (triggers auto-deploy)
- `develop` — integration branch
- `feature/*` — individual feature branches

---

## 🧗 Challenges Faced

- **ACM SSL certificate did not validate within project timeframe** — We requested an SSL/TLS certificate via AWS Certificate Manager but validation did not complete before our deadline. As a mitigation we used CloudFront's built-in HTTPS on the default `.cloudfront.net` domain, which provides full SSL encryption without requiring a custom domain certificate. In a production environment we would complete DNS validation to attach a custom domain certificate.
- ALB health check misconfiguration (resolved by fixing target group port)
- IAM permission issues during initial setup
- Security group access restrictions blocking deployment SSH
- `git checkout` conflicts due to pre-existing files in `/var/www/html` (resolved with `git checkout -f main`)

---

## 📚 Key Learnings

- AWS cloud architecture design and service integration
- Load balancing and horizontal scaling concepts
- Secure cloud deployment practices (IAM, ACM, OAC)
- CI/CD automation using GitHub Actions
- Monitoring and observability with CloudWatch
- Real-world Agile workflow with GitHub + Trello

---

## 🔭 Future Improvements

- Add Docker containerization for portability
- Use Terraform for Infrastructure as Code (IaC)
- Implement full auto-scaling with EC2 Auto Scaling Groups
- Add a database layer (RDS integration)
- Set up multi-region failover for true high availability

---

## 👥 Contributors

- Cherry Xorse Azanu
- Rebecca Batoh
- Gloria Kusi Appiah
- Amponsah Afriyie Agyare
- Mariam Lawal Addae



---


