# Day 2 – Secure EC2 Web Server + SSM Session Manager (No SSH Keys, No Port 22)  
**Date:** 02-Dec-2025  
**Student:** Shubham Chaudhary  
**Account ID:** 905418162765  
**Region:** ap-south-1 (Mumbai)


### What We Proved Today (2025 Market Gold)
| Feature                        | Why Companies Pay 50–80 LPA for This |
|--------------------------------|---------------------------------------|
| User Data scripting            | Zero manual login → full automation   |
| No SSH keys, no port 22        | Meets SOC2, ISO27001, PCI-DSS         |
| SSM Session Manager            | Audited, encrypted, IAM-controlled access |
| Private subnet access          | No bastion hosts → cleaner & safer    |
| IAM instance profile           | Least-privilege runtime permissions   |

### Resources Created
| Resource               | Name/ID                        | Subnet       | Public IP | Notes |
|------------------------|--------------------------------|--------------|-----------|-------|
| EC2 Web Server         | Web-Public-1a                  | Public-1a    | YES       | Live portfolio site |
| EC2 App Server         | App-Private-1a                 | Private-1a   | NO        | Fully isolated |
| Security Group         | Web-Tier-SG                    | –            | –         | Only 80 + 443 open |
| IAM Role               | EC2-SSM-Role                   | –            | –         | AmazonSSMManagedInstanceCore + CloudWatch |



### User Data Script (user-data.sh)
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Welcome to Shubham Chaudhary's Cloud Engineer Portfolio</h1>" > /var/www/html/index.html
echo "<p>Deployed on $(hostname -f) | $(date)</p>" >> /var/www/html/index.html
echo "<p>Instance ID: $(curl -s http://169.254.169.254/latest/meta-data/instance-id)</p>" >> /var/www/html/index.html
echo "<p>Built on Day 2 of 30-Day AWS Bootcamp | Zero SSH | SSM Only</p>" >> /var/www/html/index.html
