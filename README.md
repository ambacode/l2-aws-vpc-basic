AWS VPC Basics with Terraform

Overview
This project demonstrates building a simple AWS VPC networking environment using Infrastructure as Code (IaC) with Terraform.

The lab deploys:
A VPC with 1 public and 1 private subnet
An Internet Gateway for outbound internet access
2 EC2 instances (1 in public subnet as bastion host, 1 in private subnet)
A Security Group allowing only SSH (port 22)

Testing was completed by successfully SSH’ing into the public EC2 bastion host, then connecting from there into the private EC2 instance.

Services used:
VPC, Subnets, Internet Gateway, Route Table, Security Groups, EC2

Tools:
Terraform, AWS CLI, Git

Prerequisites:
AWS CLI configured with IAM credentials
Terraform

Steps:
git init
terraform init
terraform plan
terraform apply

Get outputs
terraform output public_instance_ip
terraform output private_instance_ip

SSH Test
Copy private key to bastion host:
scp -i ./ec2_private_key.pem ./ec2_private_key.pem ec2-user@<public_ip>:~/.ssh/

SSH into bastion:
ssh -i ec2_private_key.pem ec2-user@<public_ip>

Set permissions if needed:
chmod 400 ~/.ssh/ec2_private_key.pem

From bastion, SSH into private instance:
ssh -i ./.ssh/ec2_private_key.pem ec2-user@<private_ip>

Teardown
terraform destroy

Project Structure
.
main.tf
variables.tf
outputs.tf
ec2_private_key.pem (local only, not in repo)
README.txt

Key Learnings
Created AWS infrastructure using Terraform IaC
Implemented a bastion host to securely access private resources
Practiced configuring and testing SSH access through layered networks

References
AWS VPC Documentation: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
Terraform AWS Provider: https://registry.terraform.io/providers/hashicorp/aws/latest/docs
