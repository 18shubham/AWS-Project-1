# Day 4 – Full 3-Tier Production Architecture with Multi-AZ RDS  
**Date:** 04-Dec-2025  
**Student:** Shubham Chaudhary  
**Account ID:** 905418162765  
**Region:** ap-south-1 (Mumbai)


### Final Architecture (Exactly What Companies Run in 2025)
Internet
↓
ALB (Public subnets – 3 AZs)
↓
ASG → EC2 Web Servers (Public subnets) ← Day 3
↓ ← Secure SG reference (3306)
Multi-AZ RDS MySQL (Private subnets)
├── Primary → Private-1a
└── Standby → Private-1b (automatic failover)
└── Read Replica (optional) → Private-1c


### Live Proof
- **ALB URL:** http://ALB-Day3-xxxxxx.ap-south-1.elb.amazonaws.com  
- **RDS Endpoint:** myappdb.xxxxxxxxxxxx.ap-south-1.rds.amazonaws.com  
- **Private EC2 → RDS connection:** SUCCESS (created + read table `test` with value 999)  
- **Public web servers → RDS:** SUCCESS (db.php shows live data)

### Resources Created
| Resource               | Name / ID                             | Key Settings                            |
|-----------------------|---------------------------------------|-----------------------------------------|
| DB Subnet Group       | private-db-sg                         | Private-1a/b/c                          |
| RDS Instance          | myappdb                               | MySQL 8.0, db.t3.micro, Multi-AZ YES    |
| RDS Security Group    | RDS-SG                                | 3306 only from web SG (sg-xxx)          |
| Test Private EC2      | Private-Test-1a                       | SSM + MySQL client → successful connect |
| Web Launch Template   | Web-Simple                            | Added db.php (optional)                 |

### Proof Screenshots (in this folder)
- rds-available-multi-az.png
- rds-sg-correct-source.png
- ssm-private-ec2-db-success.png
- alb-showing-db-data.png

### What We Proved Today
- Proper network isolation (DB never public)
- Security-group-based access (not IP whitelisting)
- Multi-AZ automatic failover ready
- Full 3-tier connectivity (public web → private DB)
