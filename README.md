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
│        │                                            │                 │
│        ▼                                            ▼                 │
│  ┌───────────────┐                          ┌───────────────┐         │
│  │   EC2 (ASG)    │                          │   EC2 (ASG)    │         │
│  └───────────────┘                          └───────────────┘         │
│         ▲                                             ▲               │
│         │                                             │               │
│         └──────────────┐         ┌────────────────────┘               │
│                        ▼         ▼                                    │
│               ┌───────────────────────────┐                           │
│               │   Network Load Balancer   │                           │
│               │         (tf-nlb)          │                           │
│               └───────────────────────────┘                           │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘
```

---

## 📄 Module Breakdown

* **provider.tf**: AWS region configuration
* **vpc.tf**: VPC, subnets, route tables, and internet gateway setup
* **SecGrp.tf**: Security group allowing HTTP (80) and SSH (22) access
* **keypair.tf**: SSH keypair for EC2
* **s3.tf**: S3 bucket with IAM role/policy for EC2 access
* **iam.tf**: IAM resources to enable EC2 to interact with S3
* **launch\_template.tf**: EC2 instance config including security group, AMI, and instance profile
* **autoscaling.tf**: Auto Scaling Group with desired/min/max instance settings
* **nlb.tf**: Network Load Balancer and target group
* **variable.tf**: Input variables for customization
* **output.tf**: Output values like NLB DNS name and instance profile

---

## 🚀 Deployment

```bash
terraform init
terraform plan
terraform apply
```

---

## 🧹 Clean Up

```bash
terraform destroy
```

---

## 📌 Notes

* Ensure the S3 bucket name is globally unique and lowercase.
* The AMI ID must be valid for the specified region.
* Make sure your AWS credentials are configured properly for Terraform.

---

Let me know if you’d like a diagram export or integration with CI/CD pipelines!
