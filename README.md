You are connecting:

* Amazon S3 → stores your website files
* Amazon CloudFront → delivers content fast (CDN)
* AWS Certificate Manager → HTTPS (security)
* Amazon Route 53 → connects your domain name

---

# 🚀 Step-by-Step Flow (Beginner Friendly)

## *Step 1: Upload Website to S3*

1. Go to S3
2. Create a bucket (name = your domain, e.g., mywebsite.com)
3. Upload your files:

   * index.html
   * CSS, JS, images
4. Enable *static website hosting*

👉 Now S3 can serve your website (but not secure yet)

---

## *Step 2: Request SSL Certificate (ACM)*

1. Go to AWS Certificate Manager
2. Request a certificate for:

   * yourdomain.com
   * www.yourdomain.com
3. Choose *DNS validation*
4. ACM will give you a *CNAME record*

👉 Don’t skip this — it’s needed for HTTPS

---

## *Step 3: Validate Domain (Route 53)*

1. Open Route 53 → Hosted Zone
2. Add the *CNAME record from ACM*
3. Wait for validation (usually quick)

👉 Now your SSL certificate becomes *ACTIVE*

---

## *Step 4: Create CloudFront Distribution*

1. Go to CloudFront → Create distribution
2. Set:

   * *Origin* = S3 bucket endpoint
   * Enable *Origin Access Control (or OAI)* (secure S3)
3. Attach:

   * SSL certificate (from ACM)
4. Add:

   * Alternate domain name (your domain)

👉 Now CloudFront will:

* Serve your site
* Enable HTTPS
* Improve speed globally

---

## *Step 5: Connect Domain (Route 53)*

1. Go to Route 53 → Hosted Zone
2. Create record:

   * Type: *A (Alias)*
   * Target: CloudFront distribution

👉 This links:


yourdomain.com → CloudFront → S3


---

# 🔄 Final Flow (Simple View)


User → Domain (Route 53)
     → CloudFront (CDN + HTTPS)
     → S3 Bucket (website files)


---

# ⚠️ Important Tips

* Always use *CloudFront*, not direct S3 URL
* ACM certificate must be in *us-east-1* region for CloudFront
* Keep S3 bucket *private* (use CloudFront to access it)
* Use *Alias record*, not normal A record

---

# ✅ Your Notes vs Correct Flow

From your paper:

* ✔ S3 → correct
* ✔ ACM → correct
* ✔ Route 53 → correct
* ✔ CloudFront → correct
* ✔ CNAME validation → correct

Just remember the *order*:

👉 *S3 → ACM → Route53 (validation) → CloudFront → Route53 (final A record)*

----------------------------------------------------------------------------------------------------------------------------------------------

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
