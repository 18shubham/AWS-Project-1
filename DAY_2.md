# Day 2 – Secure EC2 Web Server + SSM Session Manager (No SSH Keys, No Port 22)  
**Date:** 02-Dec-2025  
**Student:** Shubham Chaudhary  
**Account ID:** 905418162765  
**Region:** ap-south-1 (Mumbai)


### What We Proved Today (2025 Market Gold)
| Feature                        | Dis |
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

<img width="635" height="103" alt="image" src="https://github.com/user-attachments/assets/342808aa-d129-4a9a-9004-b716da342f2f" />

<img width="887" height="353" alt="image" src="https://github.com/user-attachments/assets/f1a26974-4e6a-4716-8c1e-dd5fba8d3a68" />



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
