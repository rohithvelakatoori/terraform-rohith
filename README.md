Terraform AWS Auto Scaling Project with Launch Template, NLB, and S3 Access

This project sets up the following AWS infrastructure using Terraform:
	•	A VPC with 2 public subnets
	•	Internet Gateway and Route Table
	•	Security Group for EC2 instances
	•	Launch Template
	•	Auto Scaling Group
	•	Network Load Balancer
	•	IAM Role and Policy for EC2 to access S3
	•	S3 Bucket with unique name

⸻

File Structure

terraform-aws-autoscale/
├── autoscaling.tf
├── keypair.tf
├── launch_template.tf
├── main.tf
├── nlb.tf
├── output.tf
├── provider.tf
├── s3.tf
├── SecGrp.tf
├── variables.tf
├── vpc.tf
├── iam.tf


⸻

Prerequisites
	•	Terraform >= 1.0
	•	AWS CLI configured with necessary permissions

⸻

Usage
	1.	Clone this repo:

git clone <repo-url>
cd terraform-aws-autoscale

	2.	Initialize Terraform:

terraform init

	3.	Validate configuration:

terraform validate

	4.	Apply the infrastructure:

terraform apply

Type yes when prompted.

⸻

Components Description

provider.tf

Configures the AWS region.

variables.tf

Defines reusable variables like region, instance type, SSH CIDR, etc.

output.tf

Exports useful outputs like the NLB DNS and S3 bucket name.

vpc.tf

Creates:
	•	VPC
	•	2 public subnets
	•	Internet Gateway
	•	Route table and associations

SecGrp.tf

Creates a Security Group with:
	•	Ingress rules for SSH and HTTP
	•	Egress rule allowing all traffic

keypair.tf

Adds a key pair for EC2 access using your provided public key.

iam.tf

Creates:
	•	IAM Role with trust relationship for EC2
	•	IAM Policy to allow S3 access
	•	Attaches policy to role
	•	Instance profile for EC2

s3.tf

Creates an S3 bucket with a unique, lowercase name using random_id.

launch_template.tf

Defines:
	•	EC2 Launch Template
	•	References instance profile, security group, key pair, and AMI

autoscaling.tf

Creates:
	•	Auto Scaling Group
	•	Associates subnets and Launch Template
	•	Registers instances to Target Group

nlb.tf

Creates:
	•	Network Load Balancer
	•	Target Group
	•	Listener

⸻

Notes
	•	Ensure the ami_id variable is valid for your AWS region (you can use Amazon Linux 2).
	•	Security group allows SSH from a restricted CIDR (var.allowed_ssh_cidr).
	•	Bucket name must be globally unique and lowercase.

⸻

Cleanup

To destroy all resources:

terraform destroy

Type yes when prompted.

⸻

Authors
	•	Rohith (project setup and implementation)

⸻

License

MIT License
