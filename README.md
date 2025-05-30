# 🚀 AWS Static Website Deployment via CLI

This project demonstrates how to deploy a static website to **Amazon S3** using the **AWS CLI**, with proper configuration for **public access**, **IAM permissions**, and **budget alerts** to stay within the AWS Free Tier.

---

## 🔗 Live Demo

👉 [https://jpz-static-site-demo.s3.amazonaws.com](https://jpz-static-site-demo.s3.amazonaws.com)

Hosted entirely on a public S3 bucket using AWS Free Tier resources.

---

## 🧠 Project Goals

- Deploy a static website using **AWS CLI**
- Learn how **S3 static website hosting** works
- Set up **IAM users** and secure access
- Configure **ACLs** and **bucket policies** for public-read access
- Ensure deployment remains **within Free Tier** using **budget alerts**

---

## 🛠 Tools & Services Used

- **AWS S3** – static website hosting  
- **AWS CLI** – for terminal-based deployment  
- **IAM** – secure programmatic access  
- **ACLs & Bucket Policies** – for permissions  
- **Bash** – to run CLI commands  
- **GitHub** – documentation and visibility

---

## 🔐 AWS Account & CLI Setup

### 1. Created an IAM User
- Username: `jp-cli-deployer`
- Enabled **programmatic access**
- Attached policy: `AmazonS3FullAccess` *(for this learning project only)*  
  *(Note: In production, use scoped-down custom policies.)*

### 2. Configured AWS CLI
```bash
aws configure
````

Entered:

* **Access Key ID**
* **Secret Access Key**
* **Region**: `us-east-1`
* **Output**: `json`

Tested with:

```bash
aws s3 ls
```

---

## ⬆️ Deployment Steps

### 1. Created an S3 Bucket

* Name: `jpz-static-site-demo`
* Enabled **static website hosting**
* Set `index.html` as the entry document

### 2. Configured Public Access

* Disabled **“Block all public access”** under permissions
* Added the following **bucket policy**:

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

### 3. Synced Local Files to S3 via AWS CLI

```bash
aws s3 sync . s3://jpz-static-site-demo \
  --acl public-read \
  --exclude ".git/*" \
  --exclude "*.md" \
  --exclude ".DS_Store"
```

### 4. Confirmed Deployment

* Verified successful upload and public accessibility
* Accessed the site at:
  👉 `https://jpz-static-site-demo.s3.amazonaws.com`

---

## 💸 Budget Alert Setup (Free Tier Protection)

To ensure no unexpected charges occurred, I configured a **budget alert**:

### 1. Created a Budget

* AWS Console → Billing → Budgets → “Use a template”
* Chose **“Cost budget”**
* Set monthly threshold: `$1.00`

### 2. Configured Notifications

* Added email alerts for:

  * **80% usage** (\$0.80)
  * **100% usage** (\$1.00)
* Verified delivery of email alerts

---

## ✅ What This Project Demonstrates

* Real-world use of **AWS CLI** to manage and deploy cloud infrastructure
* Understanding of **IAM roles**, **S3 access policies**, and **ACLs**
* Awareness of **cloud cost management and budgeting**
* Familiarity with **documentation**, **command line**, and **cloud workflows**

---

## 📝 License

This project is licensed under the [MIT License](./LICENSE).

---

## 📣 Connect

Let’s connect on [LinkedIn](https://linkedin.com/in/your-profile)
Read the LinkedIn post about this project: \[Link Coming Soon]

```

---

Would you like a matching `LICENSE` file now or help writing your launch post next? You’re ready to go live with this.
```
