## Detailed Overview of Lift & Shift Web App on AWS Cloud

Deployed a multi-tier web application on AWS using Terraform to provision infrastructure. Managed EC2 instances for both web and application layers, utilized RDS for scalable database management, configured Elastic Load Balancing (ELB) for traffic distribution, and implemented Auto Scaling to dynamically adjust resources based on demand, ensuring high availability and performance.

Terraform: Terraform is an Infrastructure as Code (IaC) tool that allows us to define and provision our cloud infrastructure through configuration files. 

### Resources created in this project:
##### 1. Virtual Private Cloud (VPC):
- Definition: VPC allows you to launch AWS resources into a virtual network that we've defined.
- Usage: The web application was deployed within a VPC to ensure network isolation and security.
- Components: Subnets (public and private), Internet Gateway, NAT Gateway, Route Tables, and Network ACLs were configured to control traffic flow and enhance security.


##### 2. Elastic Cloud Compute (EC2):
- Definition: Amazon EC2 provides scalable computing capacity in the AWS cloud, allowing developers to run virtual servers (instances) to host applications. EC2 enables you to increase or decrease capacity within minutes, thus providing a flexible and cost-effective way to manage computing resources.


##### 3. Auto Scaling:
- Definition: AWS Auto Scaling helps maintain application availability by automatically adjusting Amazon EC2 capacity to match demand. It provides dynamic and scheduled scaling, health checks to replace unhealthy instances, and cost optimization by ensuring the use of necessary resources only when needed.


##### 4. Security Groups:
- Definition: Security Groups act as virtual firewalls for your Amazon EC2 instances, controlling inbound and outbound traffic. They provide stateful filtering, allowing specific traffic based on IP ranges, protocols, and ports. Security groups integrate with your Virtual Private Cloud (VPC) to enhance network security by allowing detailed access control for your instances.


##### 5. Application Load Balancer (ALB):
- Definition: The Application Load Balancer (ALB) is a managed load balancing service that operates at the application layer (Layer 7). It distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones.


##### 6. Amazon Relational Database Service (RDS):
- Definition: Amazon RDS is a managed relational database service that supports several database engines including MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB. It simplifies database management tasks such as backups, patching, and scaling.
- Components: Multi-AZ deployment for high availability, automated backups, and read replicas for improved performance.



### Project Architecture:
##### Deploying a VPC, Security Groups, EC2, ELB, Auto Scaling, RDS

![Project Diagram](https://github.com/ahsan598/aws-lift-and-shift-webapp/blob/main/aws-lift-and-shift-webapp.png)


### Environment Setup:

##### 1. Install Terraform:
- Install Terraform on your local machine or CI/CD server using the official Terraform installation instructions.
- Verify Terraform installation by running terraform --version in your terminal.
- Initialize Terraform by running terraform init in your project directory.

##### 2. Install Terraform:
- Configure AWS CLI with your AWS credentials by running aws configure in your terminal.
- Verify AWS CLI configuration by running aws sts get-caller-identity in your terminal.
- AWS Command Line Interface (CLI) allows Terraform to interact with your AWS account.
- Run `aws configure` to input your AWS access key, secret key, region, and output format.



### Implementation:

##### 1. Define the EC2 Instances (Web & Application Layers):
- Use Terraform to create EC2 instances for both the web and application layers
- EC2 (Elastic Compute Cloud) provides scalable computing capacity in AWS. The web layer will serve the frontend
(e.g., Apache, Nginx), and the app layer handles backend processing.
- EC2 instances are implicitly created through the Launch Template inside the Auto Scaling Group (asg.tf).


##### 2. Provision RDS for Database:

- Use Terraform to create an RDS (Relational Database Service) instance to manage your database.
- RDS automates database management tasks like backups, patching, and scaling, providing a scalable and reliable database layer.


##### 3. Create an Elastic Load Balancer (ELB):

- Use Terraform to create an ELB to distribute incoming traffic across multiple EC2 instances.
- ELB automatically distributes incoming traffic across multiple targets (EC2 instances), improving availability and fault tolerance.


##### 4. Set Up Auto Scaling:

- Create an Auto Scaling Group to automatically add or remove EC2 instances based on traffic demand.
- Auto Scaling ensures that the number of EC2 instances adjusts to match traffic demand, maintaining application performance and controlling costs.


##### 5. Set Up VPC, Subnets, and Security Groups:

- Define a VPC (Virtual Private Cloud), subnets, and security groups in Terraform to control the network traffic and secure your instances.
- Security Groups control inbound and outbound traffic to your instances, and VPC is used to provision a logically isolated network for your AWS resources.


##### 6. Run Terraform Commands:

After defining all the resources, run the following Terraform commands:
- `terraform init`: Initializes the Terraform project and downloads required providers.
- `terraform plan`: Creates an execution plan, showing what resources will be created.
- `terraform apply`: Applies the execution plan, provisioning the defined AWS infrastructure.