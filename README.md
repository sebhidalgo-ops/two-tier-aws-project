# two-tier-aws-project
#  Two-Tier AWS Web Application Deployment Guide

A complete, beginner-friendly walkthrough for deploying a **two-tier web application** using:
- **Amazon EC2** for the web layer (Apache + PHP + WordPress)
- **Amazon RDS (MySQL)** for the database layer (private subnet)
- **VPC Networking** with public and private subnets
- **Custom portfolio + contact form** connected to RDS

---

##  Table of Contents
1. [Overview](#overview)
2. [Architecture Diagram](#architecture-diagram)
3. [Technologies Used](#technologies-used)
4. [Setup Phases](#setup-phases)
5. [Screenshots](#screenshots)
6. [Troubleshooting](#troubleshooting)
7. [Credits](#credits)

---

##  Overview
This project demonstrates a full **AWS two-tier architecture** for small business or portfolio websites.
It includes:
- Secure private database tier  
- Publicly accessible WordPress app  
- A PHP contact form that stores user input directly into RDS.


---

##  Architecture Diagram
<img width="698" height="509" alt="image" src="https://github.com/user-attachments/assets/83dd93a9-26f4-47e8-bf4a-7afadf30d92a" />


---

##  Technologies Used
| Compute | Amazon EC2 | Web server hosting WordPress |
| Database | Amazon RDS (MySQL) | Backend data storage |
| Networking | Amazon VPC | Private/public subnet segmentation |
| IAM | AWS Systems Manager | Secure EC2 access |
| Application | WordPress + PHP | CMS and dynamic web form |

---

##  Setup Phases
### Phase 1 – Create VPC & Subnets
- CIDR: `10.0.0.0/16`
- Public Subnets: `10.0.1.0/24`, `10.0.2.0/24`
- Private Subnets: `10.0.3.0/24`, `10.0.4.0/24`

### Phase 2 – Configure Route Tables & IGW
- Create **Internet Gateway**
- Attach to VPC
- Create **Public Route Table** and associate public subnets

### Phase 3 – Launch EC2
- AMI: *Amazon Linux 2023*
- Install Apache + PHP + WordPress

### Phase 4 – Launch RDS (MySQL)
- DB Subnet Group → Private Subnets
- Disable Public Access
- Connect only from EC2 Security Group

### Phase 5 – Deploy WordPress
- Connect to RDS via `wp-config.php`
- Visit `http://<EC2-Public-IP>/` to finalize installation

### Phase 6 – Create Portfolio & Contact Page
- Deploy `portfolio.php` under `/var/www/html`
- Create `contacts` table in RDS:
  ```sql
  CREATE TABLE contacts (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(100),
      email VARCHAR(100),
      message TEXT,
      submitted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
