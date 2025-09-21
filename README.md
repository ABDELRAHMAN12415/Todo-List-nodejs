# 🛠️ DevOps Project: Automated Deployment with Ansible, Docker, and Watchtower

👋 Introduction
This project is part of a DevOps assessment. The goal is to containerize a Node.js TODO application, automate its deployment using CI/CD tools, and run it on an AWS EC2 instance with monitoring and auto-update features.
I have completed Parts 1 to 3 of the task (excluding the optional Kubernetes part), and this README documents the full process.


![chrome_VMgyYeQr3l](https://github.com/user-attachments/assets/94cc91b4-6bd5-4189-a105-c9e1cf79dea9)



---------------------------------------------------

---

## 📦 Project Stack

- **Node.js App** (sample)
- **MongoDB Atlas** (remote DB)
- **Docker & Docker Compose**
- **Ansible** (for provisioning & deployment)
- **Watchtower** (for auto-updates)
- **GitHub Actions** (for CI/CD)

---

## 🚀 Tasks & Steps

### 1. Dockerizing the App

- Dockerfile created to run a simple Node.js app
- `.dockerignore` updated to exclude unnecessary files like `node_modules`, `.env`, and Ansible config
- App exposes port `4000` inside container



---

### 2. Creating and Pushing Docker Image

- GitHub Actions used to:
  - Build image from source
  - Tag with both `latest` and `commit SHA`
  - Push to Docker Hub



---

### 3. Secure MongoDB Credentials

- Used **Ansible Vault** to encrypt MongoDB URI
- No `.env` file
- URI passed as an environment variable at runtime


---

### 4. Provisioning EC2 Instance

- Ansible playbook provisions EC2 with:
  - Docker & Docker Compose
  - Adds EC2 user to Docker group
  - copy of the docker compose file

---

### 5. Deploying with Docker Compose

- Ansible copies `docker-compose.yml` and runs it
- Mongo URI injected securely via ansible vault
- Ports mapped as `80:4000` for public access


---

### 7. Health Checks

- Added Docker health check to ensure app is running
- Checks `http://localhost:4000` every 30 seconds

---

### 6. Auto-Updating with Watchtower

- Watchtower container deployed with Docker Compose
- Monitors and auto-updates app container on new image push


<img width="2560" height="384" alt="Screenshot (3223)" src="https://github.com/user-attachments/assets/3f63178d-cba9-4bf0-bb21-f3f84f552c32" />


---

## 🌐 Final Result

The app is available on the EC2 public IP at [port 80 ](http://13.61.147.28/)  for some time

<img width="2560" height="1440" alt="Screenshot (3221)" src="https://github.com/user-attachments/assets/aa056f70-ea35-4b30-b69d-cf456ca35873" />



