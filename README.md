# aws-terraform-web-deployment

Project Overview
This project demonstrates Infrastructure as Code (IaC) using Terraform to automate the deployment of AWS infrastructure and a web server.
Instead of manually creating resources through the AWS Console, the infrastructure was provisioned declaratively using Terraform configuration files.
The deployment automatically creates networking resources, security rules, an EC2 instance, and an Nginx web page using user data.

## Architecture Flow
Internet -> Internet Gateway -> Public Subnet -> EC2 Inatance (Nginx Web Server)

*Architecture intentionally simplified to focus on Terraform fundamentals. Terraform provisions and manages all infrastructure resources.

## AWS Services & Tools Used
- Terraform
- Amazon VPC
- Public Subnet
- Internet Gateway
- Route Table
- Security Groups
- EC2
- Nginx
- AWS CLI
- VS Code

## Key Features
- Infrastructure provisioned entirely from code
- Automated EC2 deployment with Terraform
- Nginx installed automatically using user data
- Reusable configuration through Terraform variables
- Terraform outputs for EC2 public IP and DNS
- Clean infrastructure lifecycle using terraform apply and terraform destroy

## Deployment Workflow
1.	Installed and configured Terraform
2.	Configured AWS CLI credentials
3.	Created Terraform configuration files
4.	Defined VPC and public subnet
5.	Configured Internet Gateway and route table
6.	Created security group rules for HTTP and SSH
7.	Provisioned EC2 instance with Terraform
8.	Automated Nginx installation using user data
9.	Accessed deployed web application through public IP
10.	Destroyed infrastructure using Terraform destroy

## Terraform Workflow
terraform init
terraform plan
terraform apply
terraform destroy

## Challenges Encountered & Fixes
Terraform State and Old Infrastructure
Issue: Old AWS resources remained after running terraform destroy.
Cause: The older infrastructure was not tracked in the current Terraform state file.
Fix: Unused resources were manually identified and removed from the AWS Console, including:
•	EC2 instances
•	Security groups
•	Subnets
•	Internet Gateway
•	Route table
•	VPC

## Terraform Reference Errors
Issue: Terraform returned: Reference to undeclared resource
Cause: Outputs.tf referenced a resource name that did not match the resource declared in main.tf. Additionally, main.tf and other Terraform resources were accidentally created as directories instead of .tf files.
Fix: Updated resource references to match the correct Terraform resource name: resource "aws_instance" "web_server"
Removed incorrect directories, recreated proper .tf files, and reinitialized Terraform using: terraform init

## Lessons Learned
•	Terraform only manages infrastructure tracked in its state file. Resources created outside the current state may require manual cleanup.
•	Terraform-managed infrastructure differs from manual AWS deployments because resources are defined declaratively and recreated consistently through code.
•	Organizing Terraform projects into separate files (main.tf, variables.tf, outputs.tf) improves readability and maintainability.
•	Running terraform plan before terraform apply helps validate infrastructure changes and detect potential configuration issues before deployment.

## Screenshots
Deployed Website
<img width="2880" height="1800" alt="Final Website" src="https://github.com/user-attachments/assets/ef6a1f4c-cc10-481a-9981-77802f8b9cd7" />

# Terraform Apply Success + Folder Structure
<img width="2880" height="1800" alt="Terraform Apply Success" src="https://github.com/user-attachments/assets/6f8ac892-2265-4944-b511-247c36b4e70c" />

# Terraform Outputs
<img width="2880" height="1800" alt="Terraform Outputs" src="https://github.com/user-attachments/assets/f16434a7-198b-4d00-87aa-3b0c45917404" />


# Automatically Procisioned VPC Resources
<img width="2880" height="1800" alt="VPC Ressources" src="https://github.com/user-attachments/assets/e2c8f761-8502-438f-8306-27e62c57ef1a" />

## Notes
This project focused on foundational Infrastructure as Code concepts using Terraform.
The architecture was intentionally kept simple to emphasize:
•	Terraform workflow
•	Resource relationships
•	Infrastructure lifecycle management
•	Automated provisioning

Future projects will recreate the existing architecture in Terraform — ALB, ASG, and CloudWatch — replacing the manual console deployments from previous weeks with repeatable, version-controlled code.

## Next Steps
The next phase will focus on CI/CD automation using GitHub Actions.
Future improvements will include:
•	Automated deployments from GitHub to EC2
•	Continuous Integration and Continuous Deployment (CI/CD)
•	Secure deployment workflows using SSH keys and GitHub Secrets
•	Automated website updates triggered by Git commits
This will extend the project from Infrastructure as Code into deployment automation and DevOps workflows.
