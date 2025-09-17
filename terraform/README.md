# ☁️ Terraform – EC2 Provisioning on AWS

This folder contains the Terraform configuration files used to provision an AWS EC2 instance to host the Dockerized Todo List App.

![d66ee784-f56f-4ec3-b3e0-554fb40c6355](https://github.com/user-attachments/assets/1890aad0-420e-4254-84c1-ad7a0b65138a)

---

## 📌 What Does This Terraform Code Do?

- Provisions a **t2.micro** EC2 instance in your chosen AWS region  
- Attaches a **Security Group** that allows SSH and app port access (e.g., port 3000)  
- Uses your existing **key pair** to allow SSH access  
- Outputs the **public IP** of the instance so you can connect to it later using Ansible

---

## 📁 File Structure

```bash
terraform/
├── main.tf            # Main infrastructure configuration
├── backend.tf         # backend statement
├── outputs.tf         # Output values
├── provider.tf        # provider 
└── README.md          # This documentation
```
# ☁️ Terraform AWS Infrastructure – VPC + EC2 + S3 Backend

This Terraform code provisions a basic infrastructure on AWS that includes:

- A custom VPC
- A public subnet
- Internet access via an Internet Gateway
- A Security Group allowing HTTP, HTTPS, SSH, and port 4000 (for app)
- 3 EC2 instances with Apache and Python preinstalled
- An S3 bucket to be used as Terraform backend (state storage)

---

## 🌐 Architecture Overview
------------------------------
Internet
│
Internet Gateway
│
Route Table
│
Subnet (Public)
│
Security Group
│
3x EC2 Instances


---
```bash
## 🧱 Resources Created

| Resource Type        | Count | Description                             |
|----------------------|-------|-----------------------------------------|
| `aws_vpc`            | 1     | Custom VPC with CIDR `10.0.0.0/16`      |
| `aws_subnet`         | 1     | Public subnet `10.0.0.0/24`             |
| `aws_internet_gateway`| 1    | Connects VPC to internet                |
| `aws_route_table`    | 1     | Routes public traffic to IGW           |
| `aws_security_group` | 1     | Allows ports 22, 80, 443, and 4000     |
| `aws_instance`       | 3     | EC2 instances with Apache & Python     |
| `aws_s3_bucket`      | 1     | For storing Terraform state            |

---

## 🔐 Security Group Rules

| Protocol | Port  | Description                        |
|----------|-------|------------------------------------|
| TCP      | 22    | SSH access                         |
| TCP      | 80    | HTTP (for Apache or app)           |
| TCP      | 443   | HTTPS                              |
| TCP      | 4000  | Custom port (e.g., Todo app)       |

```
-------------------
🔁 S3 Backend
--------------------
An aws_s3_bucket named backend-tf-test-bucket-sallam is created for use as a Terraform backend.
To use this bucket as your remote backend, add this block to a backend.tf file:

```bash
terraform {
  backend "s3" {
    bucket = "backend-tf-test-bucket-Fortstak"
    key    = "terraform/state"
    region = "us-east-1"
  }
}
```
✅ Don't forget to run terraform init after adding this backend block.
-----------------------------------------------------------------------------------
🚀 How to Deploy
----------------------
1-Initialize Terraform
```bash
terraform init
```
2-Preview the changes
```bash
terraform plan
```
Apply the infrastructure
```bash
terraform apply
```
Destroy (after you finish)
```bash
terraform destroy
```
⚠️ Notes
-Make sure you’ve created an AWS key pair named ----- in the region before applying.

-Always use terraform plan before apply.
