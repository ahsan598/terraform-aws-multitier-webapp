## Deploying Multi-Tier Application using Terraform on AWS Cloud

Deployed a multi-tier web application on AWS using Terraform to provision infrastructure. Configured VPC for network isolation, managed EC2 instances for the application, set up Security Groups (SG) for controlled access, and utilized RDS for scalable database management, ensuring a secure and efficient deployment.

**Terraform:** Terraform is an Infrastructure as Code (IaC) tool that allows us to define and provision our cloud infrastructure through configuration files. 

### I. Resources created in this project:
##### 1. Virtual Private Cloud (VPC):
- VPC allows you to launch AWS resources into a virtual network that we've defined. The web application was deployed within a VPC to ensure network isolation and security.
- Subnets (public and private), NAT Gateway, and Security Groups were configured to control traffic flow and enhance security.


##### 2. Elastic Cloud Compute (EC2):
- Amazon EC2 provides scalable computing capacity in the AWS cloud, allowing developers to run virtual servers (instances) to host applications. EC2 enables you to increase or decrease capacity within minutes, thus providing a flexible and cost-effective way to manage computing resources.


##### 3. Security Groups:
- Security Groups act as virtual firewalls for your Amazon EC2 instances, controlling inbound and outbound traffic. They provide stateful filtering, allowing specific traffic based on IP ranges, protocols, and ports. Security groups integrate with your Virtual Private Cloud (VPC) to enhance network security by allowing detailed access control for your instances.


##### 4. Amazon Relational Database Service (RDS):
- Amazon RDS is a managed relational database service that supports several database engines including MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB. It simplifies database management tasks such as backups, patching, and scaling.



### II. Project Architecture:


            +-----------------------------+
            |       Internet Gateway      |
            +-------------+---------------+
                          |
                  +-------v--------+
                  |  Public Subnet |
                  |(Web Tier - EC2)|
                  +-------+--------+
                          |
            +-------------v-------------+
            |     Private Subnet        |
            |  (App Tier / DB - RDS)    |
            +---------------------------+

        - VPC spans multiple subnets (public & private)
        - Security Groups restrict traffic between tiers



## III. Environment Setup:

#### 1. Install Terraform:
- Install Terraform on your local machine or CI/CD server using the official Terraform installation instructions.
- Verify Terraform installation by running `terraform --version` in your terminal.


#### 2. AWS CLI Configuration:
- Configure AWS CLI with your AWS credentials in your terminal.
- Run `aws configure` to input your AWS access key, secret key, region, and output format.
- AWS Command Line Interface (CLI) allows Terraform to interact with your AWS account.


## IV. Implementation:

#### Step 1: Initialize Terraform
- Navigate to your Terraform project directory.
- Run `terraform init` to initialize Terraform and download provider plugins.


#### Step 2: Plan the Infrastructure
- Ensure all .tf files (e.g., `main.tf`, `variables.tf`, `outputs.tf`, etc.) are properly configured.
- Use terraform plan to review the resources Terraform will create.


#### Step 3: Provision VPC
- Execute `terraform apply` with only the VPC module configured to ensure networking components (VPC, subnets, etc.) are correctly created.
- Verify the created VPC and subnets in the AWS console.


#### Step 4: Add Security Groups
- Define security groups for EC2 and RDS within the respective module directories.
- Ensure appropriate ingress/egress rules are applied (e.g., open port 80 for HTTP and port 3306 for RDS).


#### Step 5: Provision EC2 Instances
- Use the outputs from the VPC module (e.g., `vpc_id`, `public_subnet_ids`) to associate EC2 instances with the VPC and subnets.
- Apply the EC2 module changes using `terraform apply`.
- Test SSH access using the provided key pair.


#### Step 6: Provision RDS
- Use the private subnets output from the VPC module (`private_subnet_ids`) for the RDS instance.
- Configure the RDS module with database parameters like `db_name`, `db_username`, and `db_password`.
- Apply the RDS module changes using `terraform apply`.
- Verify the RDS instance and connectivity.


#### Step 7: Verify Outputs
- Check the `outputs.tf` file for outputs like EC2 instance IDs, public IPs, and RDS endpoints.
- Run `terraform output` to view and validate the outputs.


#### Step 8: Test Connectivity
- Access the EC2 instance using SSH.
- Verify RDS connectivity from the EC2 instance (if required, install a MySQL client on EC2).


## V. Terraform Commands:
- `terraform init`: Initializes the Terraform project by downloading the necessary provider plugins and preparing the working directory.
- `terraform plan`: Generates and displays the execution plan, showing the resources that Terraform will create, update, or destroy without making actual changes.
- `terraform apply`: Applies the changes described in the execution plan, provisioning the resources defined in your .tf files.
- `terraform destroy`: Removes all resources that Terraform manages, as defined in your current configuration files.