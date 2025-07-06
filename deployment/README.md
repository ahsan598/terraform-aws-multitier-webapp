# 🚀 Deploying a Multi-Tier Web Application on AWS Using Terraform

This guide outlines the deployment of a multi-tier web application on AWS using Terraform for infrastructure provisioning.

---

### 📦 Architecture Overview

             +-----------------------------+
             |       Internet Gateway      |
             +-------------+---------------+
                           |
                   +-------v--------+
                   |  Public Subnet |
                   | (Web Tier EC2) |
                   +-------+--------+
                           |
             +-------------v-------------+
             |     Private Subnet        |
             |   (App / DB Tier - RDS)   |
             +---------------------------+

- **VPC** with public and private subnets
- **EC2** in public subnet (Web Tier)
- **RDS** in private subnet (DB Tier)
- **Security Groups** for traffic control

---

### 🛠️ Prerequisites:

- Terraform installed: `terraform --version`
- AWS CLI configured: `aws configure`
- **AWS IAM** user with permissions for **EC2, RDS, VPC, etc.**

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

---

### 🚧 Deployment Steps

### Step 1: Initialize Project:
- Navigate to your terraform project directory.
- Run **terraform init** to initialize terraform and download provider plugins.
```sh
terraform init
```

### Step 2: Plan the Infrastructure:
- Ensure all .tf files (e.g., `main.tf`, `variables.tf`, `outputs.tf`, etc.) are properly configured.
- Use **terraform plan** to review the resources terraform will create.
```sh
terraform plan
```

### Step 3: Provision Infrastructure
- Provision VPC, EC2, and RDS in stages or all together
- Verify the created VPC and subnets in the AWS console.
```sh
terraform apply
```

### Step 4: Validate Deployment
- SSH into EC2 instance using key pair.
- Check RDS connectivity from EC2 (`mysql -h <rds-endpoint>`).
- Access web app via EC2 public IP.


### Step 5: Verify Outputs
- Check the `outputs.tf` file for outputs like EC2 instance IDs, public IPs, and RDS endpoints.
- Run **terraform output** to view and validate the outputs.
```sh
terraform output
```
Get values like:
- EC2 Public IP
- RDS Endpoint


### Step 6: Test Connectivity
- Access EC2 Instance via SSH:
  Use the key pair specified during provisioning:
```sh
ssh -i <your-key>.pem ec2-user@<ec2-public-ip>
```
- Verify RDS Connectivity from EC2:
  1. Install MySQL client (if not already installed):
     ```sh
     sudo yum install -y mysql
     ```

  2. Connect to the RDS instance:
   ```sh
   mysql -h <rds-endpoint> -u <db-username> -p
   ```
   > You’ll be prompted to enter the database password.

- Note:
  Ensure that:
  - The RDS Security Group allows inbound traffic from the EC2 instance’s private IP or SG.
  - EC2 instance is in a public subnet with internet access (via IGW), and RDS is in a private subnet.


### Step 7: Destroy Infrastructure (Optional)
- Run **terraform destroy** in your project directory to tear down the complete infrastructure created by Terraform
```sh
terraform destroy
```

---

### ✅ Key Terraform Concepts Used
- VPC & Subnets: Network isolation and routing
- EC2: Compute instances in public subnet
- RDS: Managed database in private subnet
- Security Groups: Layered access control
- Outputs: Accessing deployed resources info


### 📘 Notes
- Ensure public/private subnet division is correct.
- NAT Gateway is used to allow private subnet internet access (for package installs, etc.).
- All credentials and secrets should be stored securely (e.g., use .tfvars and never hardcode passwords in .tf files).

---

### 🧪 Terraform Commands (Quick Overview)

- `terraform init`:
  Initializes the Terraform working directory. Downloads necessary provider plugins and sets up the backend (if configured).
- `terraform plan`:
  Generates and displays an execution plan showing what Terraform will do (create, update, delete) based on your configuration files — without making any changes.
- `terraform apply`:
  Executes the actions proposed in the plan. Provisions or updates infrastructure on AWS based on the .tf files.
- `terraform destroy`:
  Destroys all resources managed by your Terraform configuration. This command is used to clean up your AWS environment when it's no longer needed.
