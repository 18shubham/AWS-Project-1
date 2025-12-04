# Day 5 – Full Production 3-Tier App with Terraform IaC (From ZERO to LIVE in < 6 Minutes)

**Student:** Shubham Chaudhary  
**Date:** 04-Dec-2025  
**Account ID:** 905418162765  
**Region:** ap-south-1 (Mumbai)



### LIVE PROOF (Working Right Now!)
**ALB URL:** http://day5-alb-197928404.ap-south-1.elb.amazonaws.com  
**RDS Endpoint:** myappdb-tf.clyy6gyum9ld.ap-south-1.rds.amazonaws.com:3306  
**Terraform State:** Securely stored in S3 + locked with DynamoDB

### What We Built in ONE Terraform Apply
| Resource                    | Created By Terraform? | Real Production Feature |
|-----------------------------|-----------------------|--------------------------|
| Custom VPC + 6 Subnets      | Yes                   | Multi-AZ architecture   |
| NAT Gateway                 | Yes                   | Private subnet internet |
| Application Load Balancer  | Yes                   | Internet-facing + 3 AZs |
| Auto Scaling Group          | Yes                   | Min 2, Max 4, auto-healing |
| Launch Template + User Data | Yes                   | Apache + PHP auto-install |
| Multi-AZ RDS MySQL          | Yes                   | Automatic failover < 2 min |
| Security Groups            | Yes                   | Least privilege (finally fixed!) |
| Remote State + Locking      | Yes                   | Team-ready, no conflicts |

### Terraform Files (Professional Structure)

aws-30days-terraform/
├── backend.tf           → S3 + DynamoDB (production-ready)
├── provider.tf          → AWS + profile day1
├── variables.tf         → db_password
├── main.tf              → ENTIRE 3-tier stack
├── outputs.tf           → ALB & RDS endpoint
└── data "aws_ami"       → Always latest Amazon Linux 2023


### Commands That Built Everything
```bash
terraform init -upgrade -reconfigure
terraform fmt -recursive
terraform validate
terraform apply -auto-approve    # ← MAGIC COMMAND (6 minutes)
