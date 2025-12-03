# Day 3 – High-Availability 2-Tier Web App with ALB + Auto Scaling  
**Date:** 03-Dec-2025  
**Student:** Shubham Chaudhary  
**Account ID:** 905418162765  
**Region:** ap-south-1 (Mumbai)


### Final Architecture (Production-Grade 2025)
Internet
↓
Application Load Balancer (Prod-ALB) → 3 AZs
↓
Target Group (Web-TG-OK) → health checks on /
↓
Auto Scaling Group (Web-ASG)
├── Min 2 / Desired 2 / Max 6
├── Spread across Public-1a, Public-1b, Public-1c
└── Launch Template: Web-Simple (latest version)
├── Amazon Linux 2023 + Apache (User Data)
├── SSM Role (no SSH keys)
└── Security Group: DAY3-FIX (temporary permissive) → later Web-Tier-SG


### Live Demo (Working!)
**ALB URL:** http://prod-alb-730053987.ap-south-1.elb.amazonaws.com  
(Refresh multiple times → see different Instance IDs & AZs → proof of load balancing + scaling)

### Key Resources Created
| Resource               | Name / ID                                 | Purpose                              |
|-----------------------|-------------------------------------------|--------------------------------------|
| VPC                   | Prod-VPC-2025                             | Custom isolated network              |
| Subnets               | Public-1a/b/c                             | Multi-AZ web tier                    |
| ALB                   | Prod-ALB                                  | Internet-facing load balancer        |
| Target Group          | Web-TG-OK                                 | Health checks + routing              |
| Launch Template       | Web-Simple (latest version)               | Golden image + User Data             |
| Auto Scaling Group    | Web-ASG                                   | Auto-scale + self-healing            |
| Security Group        | DAY3-FIX (temporary) → later Web-Tier-SG  | Port 80 open                         |

### User Data Script (Web-Simple)
```bash
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello from Shubham – Simple Template Works!</h1>" > /var/www/html/index.html
echo "<p>Instance: $(hostname)</p>" >> /var/www/html/index.html
