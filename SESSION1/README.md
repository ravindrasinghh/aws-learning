# 🌥️ AWS IAM, EC2, and Website Hosting Demo

This guide includes:
- IAM user & group setup
- EC2 IAM role & S3 access
- Web hosting in NGINX (Linux EC2)
- Web hosting in IIS (Windows EC2)

---

## 🔐 IAM Setup

### 1. Create IAM User with Programmatic Access
1. Go to AWS Console → IAM → Users → Add User
2. Username: `cli-user`
3. Access type: ✅ Programmatic Access
4. Attach Policy: `AmazonS3ReadOnlyAccess` (or create custom)
5. Save the **Access Key ID** and **Secret Access Key**

---

### 2. Configure AWS CLI with These Keys

```bash
aws configure
# Enter Access Key, Secret, region (e.g., ap-south-1), and output format (json)
```
---

###  3. Verify Access (Try Listing Buckets)
``` bash
aws s3 ls
```
---
### 🌥️ 🌐 Hosting a Website with NGINX (Amazon Linux EC2)

 -🪄 EC2 Launch Steps:
- Amazon Linux 2
- t2.micro (Free Tier)
- Security Group: Allow Port 22 (SSH) & 80 (HTTP)

``` bash
sudo apt update
sudo apt install nginx -y
cd /var/www/html/
touch index.html > Welcome to the World
sudo systemctl restart nginx
```


➡️ Access site using Public IP in browser.
---

### 🪟 Hosting a Website on IIS (Windows EC2)
🪄 EC2 Launch Steps:
- Choose Windows Server 2019/2022 Base
- t2.micro
- Security Group: Allow RDP (3389) & HTTP (80)

- 📜 PowerShell Script (for User Data or Run Manually)

```bash
Install-WindowsFeature -name Web-Server -IncludeManagementTools
Set-Content -Path "C:\inetpub\wwwroot\index.html" -Value "<h1>Hello from IIS on Windows EC2</h1>"
➡️ RDP into the instance and open http://<Public-IP> to view the site.
```
