# AWS-3-TIER-ARCHITECTURE-PROJECT
# Deploying a 3-Tier Architecture on AWS

This project demonstrates the manual deployment of a 3-tier architecture on AWS for an open-source Netflix clone. The architecture consists of a web tier, an application tier, and a database tier, integrated with various AWS resources.

## Steps to Deploy

### Step 1: Downloading the Code from GitHub
- Cloned the repository from GitHub to my local system.

### Step 2: Creating S3 Buckets
- Created two S3 buckets:
  1. One for storing web-server & app-server code and uploaded the necessary files.
  2. Another for storing VPC flow logs.

### Step 3: Creating IAM Roles with Policies
- Created an IAM role with the following policies:
  - **S3 Read-Only Access**
  - **SSM Managed Instance Core** (for connecting instances using SSM)

### Step 4: Setting Up Networking (VPC, Subnets, IGW, NAT Gateway, Route Tables)
- Created a VPC with public and private subnets.
- Enabled auto-assign public IP for web-tier subnets.
- Configured Internet Gateway (IGW) and NAT Gateway for internet access.
- Created flow logs for VPC and stored them in the S3 bucket.

### Step 5: Configuring Security Groups
- **External Load Balancer SG:** Allowed HTTP (80) from the internet.
- **Web Tier SG:** Allowed HTTP (80) from the External Load Balancer.
- **Internal Load Balancer SG:** Allowed HTTP from the Web Tier.
- **App Tier SG:** Allowed port 4000 from the Internal Load Balancer.
- **Database Tier SG:** Allowed MySQL (3306) access from the App Tier.

### Step 6: Creating DB Subnet Group & RDS
- Created a DB subnet group.
- Launched an RDS instance (Multi-AZ) within the DB subnet group.
- Connected RDS using **SSM Manager and IAM roles** instead of direct database user access.

### Step 7: Deploying the Application Tier
- Launched a test App Server to install necessary packages and test connections.
- Created an **AMI** of the configured App Server.
- Created a launch template using the AMI.
- Created a **Target Group** and an **Internal Load Balancer**.
- Configured an **Auto Scaling Group** for the application tier.
- Edited `nginx.conf` in my local system to add the **Internal Load Balancer DNS** and uploaded the file to S3.

### Step 8: Deploying the Web Tier
- Launched a test Web Server and installed required packages (Nginx, Node.js (React)).
- Created an **AMI** of the configured Web Server.
- Created a launch template using the AMI.
- Created a **Target Group** and an **External Load Balancer**.
- Configured an **Auto Scaling Group** for the web tier.

### Step 9: Configuring DNS in Route 53
- Added **External Load Balancer DNS** as a record in Route 53 for domain resolution.

### Step 10: Monitoring with CloudWatch & SNS
- Created **CloudWatch Alarms** for monitoring instances and other AWS resources.
- Integrated **SNS** for alert notifications.

### Step 11: Enabling CloudTrail
- Enabled **AWS CloudTrail** to track API activity and security-related events.

### Step 12: Deleting the Infrastructure
- Successfully deleted all AWS resources in a structured manner, including EC2 instances, Load Balancers, RDS, S3 buckets, and networking components.

## Outcome
This project helped me gain hands-on experience in manually deploying a 3-tier architecture using AWS services. By integrating IAM, S3, VPC, EC2, ALB, Auto Scaling, RDS, Route 53, CloudWatch, SNS, and CloudTrail, I successfully deployed and managed a scalable web application.

---

This README serves as a step-by-step guide for deploying a 3-tier architecture manually on AWS based on my implementation.
