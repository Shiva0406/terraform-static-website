1. Prerequisites (Must Do Before Terraform)
1. Install tools

Install:

Terraform
AWS CLI
Git

Check:

terraform -v
aws --version
2. Configure AWS
aws configure

Enter:

AWS Access Key
AWS Secret Key
Region (example: ap-south-1)
Output: json
3. Domain Must Exist

Your domain must already exist (example):

yourdomain.com

If using external registrar (Hostinger etc.), you will later point nameservers to Route53.

4. Create Hosted Zone in Route53

Go to AWS → Route53 → Hosted Zones → Create Hosted Zone

Copy:

Hosted Zone ID
Nameservers

Update nameservers in your domain registrar.

Wait until DNS propagates.

2. Project Structure
terraform-static-website/
│
├── provider.tf
├── variables.tf
├── locals.tf
├── s3.tf
├── acm.tf
├── cloudfront.tf
├── route53.tf
├── s3-policy.tf
├── outputs.tf
└── terraform.tfvars
