# Terraform AWS Autoscaling Infrastructure

## 🔧 Project Overview

This project uses Terraform to provision a scalable AWS infrastructure including:

* **VPC** with public subnets
* **Internet Gateway** and **Route Tables**
* **Security Group** with SSH and HTTP access
* **Key Pair** for EC2 instance access
* **Launch Template** for EC2 configuration
* **Auto Scaling Group** for dynamic instance management
* **Network Load Balancer** to distribute traffic
* **IAM Role and S3 Policy** to allow EC2 to access an S3 bucket

---

## 📐 Architecture Summary

```text
                                   ┌────────────────────┐
                                   │     S3 Bucket      │
                                   │  (tf-s3 bucket)    │
                                   └────────┬───────────┘
                                            │
                                            ▼
                                  ┌────────────────────┐
                                  │   IAM Role +       │
                                  │ Instance Profile   │
                                  └────────┬───────────┘
                                           │
                                           ▼
┌───────────────────────────────────────────────────────────────────────┐
│                             AWS VPC (tf-vpc)                          │
│                                                                       │
│  ┌────────────────────┐                    ┌────────────────────┐     │
│  │  Public Subnet A   │                    │  Public Subnet B   │     │
│  └────────────────────┘                    └────────────────────┘     │
│        │                                            │
```
