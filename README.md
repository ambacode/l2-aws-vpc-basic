create .gitignore

git init

terraform init

vscode to create variables.tf and main.tf

terraform plan

terraform apply

get public ip for public ec2:
terraform output ec2_public_ip

get private ip for private ec2:
terraform output ec2_private_ip

keypair will be saved locally to working dir:
ec2_private_key.pem
! note for the sake of simplicity we are using the same keypair for both ec2 instances

copy private key to public ec2 bastion host
scp -i ./ec2_private_key.pem ./ec2_private_key.pem ec2-user@<ec2 public ip>:~/.ssh/

ssh to public ec2
ssh -i ec2_private_key.pem ec2-user@<ec2 public ip>

set permissions for key file on bastion host if necessary
chmod 400 ~/.ssh/ec2_private_key.pem

ssh to private ec2
ssh -i ./.ssh/ec2_private_key.pem ec2-user@<ec2 private ip>

then tear it all down:
terraform destroy