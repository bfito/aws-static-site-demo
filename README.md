# 🚀 AWS Static Website Deployment via CLI

This project demonstrates how to deploy a static website to **Amazon S3** using the **AWS CLI**, with proper configuration for **public access**, **IAM permissions**, and **budget alerts** to stay within the AWS Free Tier.

---

## 🔗 Live Demo

[🔗 Live Demo (via CloudFront)](https://d3d14snt9uqisf.cloudfront.net/)

Here’s your **complete, updated write-up** with the CloudFront section fully integrated and the correct **origin domain note** added. It’s ready for use in your GitHub `README.md`:

---

# 🚀 AWS Static Website Deployment via CLI + CloudFront

This project demonstrates how to deploy a static website to Amazon S3 using the AWS CLI, with proper configuration for public access, IAM permissions, and budget alerts to stay within the AWS Free Tier.

🔗 **Live Demo**
🔗 **Live Demo (via CloudFront)**

Hosted entirely on a public S3 bucket using AWS Free Tier resources, then served securely and globally through **Amazon CloudFront** for enhanced performance and protection.

---

## 🧠 Project Goals

* Deploy a static website using AWS CLI
* Learn how S3 static website hosting works
* Set up IAM users and secure access
* Configure ACLs and bucket policies for public-read access
* Serve content globally using CloudFront CDN
* Ensure deployment remains within Free Tier using budget alerts

---

## 🛠 Tools & Services Used

* **AWS S3** – static website hosting
* **AWS CloudFront** – global CDN and HTTPS support
* **AWS CLI** – for terminal-based deployment
* **IAM** – secure programmatic access
* **ACLs & Bucket Policies** – for permissions
* **Bash** – to run CLI commands
* **GitHub** – documentation and visibility

---

## 🔐 AWS Account & CLI Setup

1. **Created an IAM User**

   * Username: `jp-cli-deployer`
   * Enabled programmatic access
   * Attached policy: `AmazonS3FullAccess` (for this learning project only)
     *Note: In production, use scoped-down custom policies.*

2. **Configured AWS CLI**

   ```bash
   aws configure
   ```

   Entered:

   * Access Key ID
   * Secret Access Key
   * Region: `us-east-1`
   * Output format: `json`

   Tested access with:

   ```bash
   aws s3 ls
   ```

---

## ⬆️ Deployment Steps

1. **Created an S3 Bucket**

   * Name: `jpz-static-site-demo`
   * Enabled static website hosting
   * Set `index.html` as the entry document

2. **Configured Public Access**

   * Disabled “Block all public access” under bucket permissions
   * Added the following bucket policy:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [{
       "Sid": "PublicReadGetObject",
       "Effect": "Allow",
       "Principal": "*",
       "Action": "s3:GetObject",
       "Resource": "arn:aws:s3:::jpz-static-site-demo/*"
     }]
   }
   ```

3. **Synced Local Files to S3 via AWS CLI**

   ```bash
   aws s3 sync . s3://jpz-static-site-demo \
     --acl public-read \
     --exclude ".git/*" \
     --exclude "*.md" \
     --exclude ".DS_Store"
   ```

4. **Confirmed Deployment**

   * Verified successful upload and public accessibility
   * Accessed the site at: 👉 `https://jpz-static-site-demo.s3.amazonaws.com`

---

## 🌐 CloudFront Integration (CDN + HTTPS)

To serve the S3-hosted site via a global CDN and support HTTPS:

1. **Created a CloudFront Distribution**

   * **Origin Domain Name**: `jpz-static-site-demo.s3-website-us-east-1.amazonaws.com`
   * ⚠️ *Note: When using an S3 static website, you **must** select the S3 **Website Endpoint** (not the default S3 bucket name) as the origin.*
   * Origin Type: **S3 Website**
   * Viewer Protocol Policy: **Redirect HTTP to HTTPS**
   * Default Root Object: `index.html`

2. **Disabled Bucket Access Logging** (optional for Free Tier)

3. **Noted the CloudFront Distribution URL**

   * Example: `https://d1234abcd.cloudfront.net`
   * Shared publicly as alternate live demo link

4. *(Optional)* **Custom Domain & HTTPS via ACM**
   For future improvements, a custom domain and SSL certificate via **AWS Certificate Manager (ACM)** can be added.

---

## 💸 Budget Alert Setup (Free Tier Protection)

To ensure no unexpected charges occurred, I configured a billing budget alert:

1. **Created a Budget**

   * AWS Console → Billing → Budgets → “Use a template”
   * Chose **Cost budget**
   * Set monthly threshold: `$1.00`

2. **Configured Notifications**

   * Email alerts for:

     * 80% usage (\$0.80)
     * 100% usage (\$1.00)
   * Verified email delivery

---

## ✅ What This Project Demonstrates

* Real-world use of AWS CLI to manage and deploy cloud infrastructure
* Understanding of IAM roles, S3 access policies, and ACLs
* Global CDN integration via CloudFront
* Awareness of cloud cost management and Free Tier usage
* Familiarity with documentation, shell scripting, and cloud workflows

---

## 📝 License

This project is licensed under the **MIT License**.

---

Let me know if you want a Markdown file (`README.md`) version or want to add badges like `AWS`, `HTML5`, or `MIT Licensed`.
