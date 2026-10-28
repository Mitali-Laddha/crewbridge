# CrewBridge — Contract & Gig Worker Management Platform

A comprehensive, cloud-native platform built on Amazon Web Services (AWS) designed to streamline contract worker onboarding, identity verification, job application approvals, time tracking, and automated payroll processing.

---

## 📌 Project Overview

Managing contract and gig workers often involves fragmented email threads, manual identity checks, and error-prone spreadsheets for payroll. **CrewBridge** centralizes this lifecycle into a single secure platform:
- **Workers** register, upload identity documents, apply for open job slots, and log worked hours.
- **Managers** verify AI-flagged identity documents, approve job applications and timesheets, and execute automated payroll runs.

---

## 🛠️ Key Features & AWS Architecture

The platform leverages **24 AWS services** across serverless, auto-scaling, and event-driven architectures:

### 1. 🔑 Identity & Access Management
* **Amazon Cognito:** Manages user authentication, account registration, role-based access control (Workers vs. Managers), and JWT token generation with optional MFA.

### 2. 🪪 AI-Powered Identity Verification
* **Amazon S3 & Presigned URLs:** Secure, direct client-to-S3 document uploads with temporary 5-minute pre-signed URLs.
* **AWS Lambda & Amazon Textract:** Automatic execution triggered by S3 upload events. Textract's `AnalyzeID` parses passports and driver's licenses, extracts metadata, masks sensitive fields (keeping only the last 4 digits), and flags discrepancies for manager approval.

### 3. 🌐 Scalable Web Tier
* **Amazon EC2 Auto Scaling:** Dynamic web cluster running Nginx (scaling between 2 to 6 instances across 2 Availability Zones).
* **AWS CloudFront & Application Load Balancer (ALB):** Global CDN delivery with HTTPS termination and custom header secret checks to restrict direct ALB bypass.
* **AWS WAF:** Web Application Firewall guarding against common exploits and rate-limiting abusive IP addresses.

### 4. ⚡ Serverless API & Data Layer
* **Amazon API Gateway:** HTTP API with integrated JWT authorization and request throttling.
* **AWS Lambda:** Serverless microservices executing all core business logic (jobs, hours, approvals).
* **Amazon DynamoDB:** 5 on-demand database tables with Global Secondary Indexes, Point-in-Time Recovery (PITR), and conditional writes for concurrency control.

### 5. 💰 Automated Payroll Engine
* **Amazon EventBridge:** Scheduled cron job triggering weekly payroll calculation functions (every Monday at 02:00 UTC).
* **S3 Export:** Payroll outputs generated in both CSV and JSON formats with duplicate-payment protection.

### 6. 🔒 Security, Backups & Observability
* **AWS KMS & IAM:** Encryption at rest for data buckets and DynamoDB, adhering strictly to least-privilege permissions.
* **Amazon CloudWatch & AWS X-Ray:** Centralized dashboards, request tracing, and 18 operational alarms configured with SNS notification topics.
* **AWS Backup & CloudTrail:** Automated daily/weekly/monthly backup policies and complete API audit logging.

---

## 👥 Authors

* **Isha Gawande** (Roll No. 1032233333)
* **Mitali Laddha** (Roll No. 1032232905)

---

## 📄 License

This project was developed as part of an academic AWS Cloud Computing coursework.
