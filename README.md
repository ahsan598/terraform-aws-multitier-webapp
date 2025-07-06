# 🌐 Multi-Tier Web Application Deployment on AWS using Terraform

This project demonstrates how to deploy a **multi-tier web application on AWS** using **Terraform** for Infrastructure as Code (IaC). The architecture includes a **frontend and backend** hosted on **EC2 instances**, with a **managed RDS database**, all secured and isolated within a custom **VPC**.


### 🧰 Tools & Technologies Used

| Tool / Service | Purpose                                                           |
|----------------|-------------------------------------------------------------------|
| Terraform      | Infrastructure as Code (IaC) to provision AWS resources           |
| AWS VPC        | Provides isolated networking environment for the app              |
| AWS EC2        | Hosts the frontend and backend application servers                |
| AWS RDS        | Managed relational database service (e.g., MySQL or PostgreSQL)   |
| Security Groups| Acts as a virtual firewall to control inbound and outbound access |
| AWS IAM        | Manages roles and permissions                                     |

---

### 📌 Project Objectives

- Automate AWS infrastructure provisioning using Terraform
- Deploy a scalable and secure **multi-tier architecture**
- Practice **Infrastructure as Code** (IaC) using best practices
- Understand real-world cloud components like **VPC, EC2, RDS, Security Groups**

---

### 🗂️ Project Structure

```
multi-tier-terraform/
├── main.tf                # Calls modules and connects everything
├── variables.tf           # Input variables for main config
├── outputs.tf             # Outputs from modules
├── terraform.tfvars       # Values for the variables
├── modules/               # Reusable modules
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── ec2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── rds/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── README.md              # Project documentation
```


### ⚙️ What This Project Does

1. **Creates a custom VPC** with public and private subnets.
2. **Launches EC2 instances** in the public subnet for frontend/backend.
3. **Configures Security Groups** to:
   - Allow HTTP (port 80) access from the internet to EC2
   - Allow EC2 to access RDS on port 3306 (or 5432 for PostgreSQL)
4. **Deploys an RDS instance** in the private subnet.
5. Outputs useful details like public IP of **EC2 and DB endpoint**.

---

### 🧱 Architecture Overview

![Project Diagram](https://github.com/ahsan598/terraform-aws-webapp-stack/blob/main/multi-tier%20app.png)

---

### 🚀 How to Run This Project Locally (For Practice)

> Make sure you have [Terraform](https://developer.hashicorp.com/terraform/downloads) and an [AWS account](https://aws.amazon.com/) with configured credentials (`aws configure`).

### Step 1: Clone the repository
```bash
git clone https://github.com/yourusername/multi-tier-terraform.git
cd multi-tier-terraform
```

### Step 2: Initialize Terraform
```bash
terraform init
```

### Step 3: Review and apply the plan
```bash
terraform plan
terraform apply
```

### Step 4: Confirm outputs
#### Terraform will display outputs like:
```bash
ec2_public_ip = "13.234.56.78"
rds_endpoint  = "mydb.xxxxxx.us-east-1.rds.amazonaws.com"
```

### Step 5: Clean up (Optional)
```bash
terraform destroy
```

---

### 🧠 What You’ll Learn
- Building real-world infrastructure using Terraform modules
- Using input variables and outputs efficiently
- Structuring Terraform projects for clarity and reusability
- Understanding cloud networking and tiered architecture
- Applying security best practices with IAM and SGs


### 💡 Ideas to Extend This Project
- Add Bastion Host or NAT Gateway for private subnet access
- Use Terraform Cloud or S3 backend for remote state management
- Integrate with Ansible or Jenkins for app deployment
- Deploy autoscaling groups and load balancer (ALB)


### 📚 Resources to Learn More
- [Terraform AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Terraform VPC Tutorial](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-create)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [Learn Terraform Modules](https://developer.hashicorp.com/terraform/language/modules)

---

🛠️ **This is a personal project aimed at learning purposes**