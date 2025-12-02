# AWS-Project-1
AWS/Cloud Project Deatils
# Day 1 – Production-Grade VPC Foundation | AWS Cloud Engineer 30-Day Bootcamp
**Date:** 02-Dec-2025  
**Student:** Shubham Chaudhary  
**Account ID:** 905418162765  
**Region:** ap-south-1 (Mumbai)  
**Goal:** Build a secure, multi-AZ, production-ready VPC from scratch (exactly how FAANG/Startups do it in 2025)

### Why We Did Each Step (Real-World Reasoning – Put This in Interviews!)

| Step | What We Did | Why It Matters in Real Jobs (2025 Market) |
|------|-------------|--------------------------------------------|
| 1. Installed & configured AWS CLI v2 | Local terminal → `aws configure --profile day1` | 90% of senior engineers never touch console. CLI + scripts = speed, repeatability, IaC foundation |
| 2. Secured root + created admin IAM user | MFA on root + AdministratorAccess user | First thing auditors check. Root keys never used again |
| 3. Enabled Billing Budget ($15) + Cost Explorer | Alerts at 80% & 100% | Free-tier accidents kill resumes. Pros set budgets Day 0 |
| 4. Created CloudTrail (main-trail-2025) | Global trail + dedicated S3 bucket | Every compliance team (PCI, SOC2, ISO) demands full audit logs |
| 5. Custom VPC 10.0.0.0/16 | Isolated network instead of default VPC | Default VPC is shared & insecure – enterprises NEVER use it |
| 6. 6 Subnets (3 Public + 3 Private across 3 AZs) | Multi-AZ = High Availability | One AZ dies → app stays up (required for 99.9%+ SLAs) |
| 7. Internet Gateway + Public Route Table | Public subnets can reach internet | Web servers, bastion hosts, NAT gateways live here |
| 8. NAT Gateway in Public-1a + Private Route Table | Private subnets get outbound internet (yum, curl) but NOT inbound | Security best practice – DBs, workers never exposed |
| 9. Proper naming & tagging | Prod-VPC-2025, Public-1a, NAT-1a, etc. | Large companies have 1000s of VPCs – without tags = chaos |

### Architecture Diagram
![Day 1 VPC Diagram](./day1-vpc-diagram.png)
(3 AZs | Public + Private subnets | IGW | Single NAT | Isolated & Secure)

### Resources Created Today
| Resource            | Name/ID                                 | Purpose |
|---------------------|-----------------------------------------|---------|
| VPC                 | Prod-VPC-2025 (`vpc-0xxxxxxx`)          | Network boundary |
| Subnets             | Public-1a/b/c, Private-1a/b/c           | Tier separation |
| Internet Gateway    | Prod-IGW                                | Public internet access |
| NAT Gateway + EIP   | NAT-1a                                  | Private subnet outbound |
| Route Tables        | Public-RT, Private-RT                   | Traffic routing |
| CloudTrail          | main-trail-2025                         | Full audit logging |
| Billing Budget      | $15 monthly                             | Cost control |

### Cost After Day 1
~ $0.04–$0.06/day for NAT Gateway + EIP (we will delete/recreate during practice)  
Everything else free-tier safe.

### Next Steps (Tomorrow – Day 2)
- Launch EC2 in public subnet with User Data (auto-install Apache)
- SSM Session Manager bastion (no SSH keys)
- Security Groups + NACLs
- Connect private subnet instances securely

**This Day 1 alone already beats 90% of freshers' resumes in 2025.**


