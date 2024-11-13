##Github action AWS infra with Terraform:

![alt text](image.png)

Automating AWS VPC Deployment with EC2 using GitHub Actions and Terraform Cloud
In this lab, you will learn how to automate the deployment of an AWS infrastructure using Terraform and GitHub Actions. The infrastructure includes a Virtual Private Cloud (VPC) with a public subnet, an Internet Gateway (IGW), and an EC2 instance. The SSH public key used to access the EC2 instance will be securely managed using GitHub Secrets, and the Terraform state file will be stored in Terraform Cloud to ensure consistency and security across deployments.


##Objectives:


By the end of this lab, you will be able to:

Automate the deployment of an AWS VPC with a public subnet using Terraform and GitHub Actions.
Securely manage and store an SSH public key using GitHub Secrets.
Deploy an EC2 instance within the public subnet.
Store and manage the Terraform state file in Terraform Cloud.
Output key information such as the EC2 instance’s public IP, VPC ID, Subnet ID, and Security Group ID.

##Prerequisites:


Before starting this lab, ensure you have the following:

-GitHub Account: A GitHub account to store your project and manage secrets.
-Terraform Cloud Account: A Terraform Cloud account to manage the Terraform state file.
-AWS Account: An AWS account with permissions to create and manage VPCs, EC2 instances, and related resources.
-SSH Key Pair: An SSH key pair (id_rsa and id_rsa.pub) generated on your local machine.


##Scenario:

You're tasked with automating the deployment of an AWS VPC with a public subnet and an EC2 instance using Terraform. The infrastructure will be defined in Terraform, with the state file stored in Terraform Cloud, and the deployment automated through GitHub Actions. SSH keys will be securely managed with GitHub Secrets to protect sensitive data. By the end, you'll have an automated pipeline that deploys the infrastructure on every GitHub push.

##Project directory structure for the lab:

terraform-aws-vpc-github-actions/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── main.tf
├── variables.tf
└── outputs.tf

##Lab Steps:

Step 1: Terraform Cloud Setup
1. Create a Terraform Cloud Project
Sign in to Terraform Cloud.
Navigate to your organization.
Go to "Projects" and click "New Project".
Name your project (e.g., "poridhi-terraform") and click "Create Project".

2. Create a Workspace
Within your project, go to the "Workspaces" tab.
Click "New Workspace".
Choose "CLI-driven workflow".
Name your workspace (e.g., "vpc-workspace") and click "Create Workspace".

3. Generate a Terraform Cloud API Token
Go to User Settings (top-right corner).
Under "Tokens", click "Create an API Token".
Name your token and click "Create".
Copy the token and add it to your GitHub Secrets as TF_CLOUD_TOKEN.

##Step 2: Setting Up the VPC and Public Subnet

Create the Terraform Configuration Files
Create the following files in your project directory:

main.tf: Contains the main configuration for setting up the VPC, subnet, security group, key pair, and EC2 instance.

variables.tf: Defines the variables used in the main.tf file, including the SSH public key.

outputs.tf: Specifies the outputs from your Terraform configuration, such as the public IP, VPC ID, Subnet ID, and Security Group ID.

##Step 2: Setting Up GitHub Actions:

2.1 Store AWS Credentials and SSH Keys in GitHub Secrets:

Generate SSH Keys (if you haven't already):
--"ssh-keygen -t rsa -b 4096 -C "your_email@example.com""

This generates a private key (id_rsa) and a public key (id_rsa.pub) in the ~/.ssh/ directory.

**Store Secrets:

-Navigate to your GitHub repository.

-Go to Settings > Secrets and variables > Actions > New repository secret.

Add the following secrets:

1.AWS_ACCESS_KEY_ID: Your AWS access key ID.
2.AWS_SECRET_ACCESS_KEY: Your AWS secret access key.
3.SSH_PRIVATE_KEY: Paste the contents of your id_rsa file in ~/.ssh directory.
4.SSH_PUBLIC_KEY: Paste the contents of your id_rsa.pub in ~/.ssh directory.
5.TF_CLOUD_TOKEN: Add the Terraform Cloud API token as a secret.

2.2 Create a GitHub Actions Workflow:

Create a .github/workflows/deploy.yml file in your repository with the following content: