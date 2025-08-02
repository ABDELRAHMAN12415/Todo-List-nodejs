# 🛠️ DevOps Project: Automated Deployment with Ansible, Docker, and Watchtower

This project demonstrates a CI/CD workflow using **GitHub Actions**, **Docker**, **Ansible**, and **Watchtower**, deployed on an **AWS EC2** instance.

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

<img width="594" height="293" alt="image" src="https://github.com/user-attachments/assets/1bd20426-c174-4eb3-8b58-8a77cb91c079" />
<img width="1029" height="567" alt="image" src="https://github.com/user-attachments/assets/f51ccbe3-ded6-4092-ad19-8c56311fdc1c" />


---

### 2. Creating and Pushing Docker Image

- GitHub Actions used to:
  - Build image from source
  - Tag with both `latest` and `commit SHA`
  - Push to Docker Hub

<img width="1220" height="820" alt="Screenshot 2025-08-02 081338" src="https://github.com/user-attachments/assets/a20d9fae-2f2c-4e6d-b2ec-d0e19639c583" />



---

### 3. Secure MongoDB Credentials

- Used **Ansible Vault** to encrypt MongoDB URI
- No `.env` file included in the container
- URI passed as an environment variable at runtime


---

### 4. Provisioning EC2 Instance

- Ansible playbook provisions EC2 with:
  - Docker & Docker Compose
  - Adds EC2 user to Docker group

<img width="2560" height="1440" alt="Screenshot (3217)" src="https://github.com/user-attachments/assets/2bee5ca1-cfe0-4af2-bcbd-8d00d1ae9278" />
<img width="910" height="264" alt="image" src="https://github.com/user-attachments/assets/62a3db95-0c92-4bf5-8e8c-fd1486712c0b" />


---

### 5. Deploying with Docker Compose

- Ansible copies `docker-compose.yml` and runs it
- Mongo URI injected securely via environment variable
- Ports mapped as `80:4000` for public access
- 

<img width="673" height="550" alt="Screenshot 2025-08-02 081403" src="https://github.com/user-attachments/assets/6b0775a8-c1f6-4ad2-9ee1-6106a075988e" />


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
- inpound rule for http
<img width="2556" height="680" alt="Screenshot (3222)" src="https://github.com/user-attachments/assets/d66dfe0f-f303-4a95-b204-195e6399852b" />


---

## 📝 Notes

- MongoDB used is hosted externally (MongoDB Atlas)
- bonus Kubernetes task was skipped as it was hard to install on freetier t2.micro instance


