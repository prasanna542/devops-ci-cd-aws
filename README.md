# 🚀 End-to-End CI/CD Pipeline using GitHub Actions, Terraform, Ansible & AWS EC2

This project demonstrates a complete **real-world DevOps CI/CD pipeline** that automates the entire application lifecycle — from code commit to deployment on AWS EC2.

The project focuses on **industry-standard DevOps practices** such as Infrastructure as Code, automated testing, containerization, and configuration management.

---

## 🛠️ Tech Stack

- **CI/CD**: GitHub Actions  
- **Containerization**: Docker  
- **Infrastructure as Code**: Terraform  
- **Configuration Management**: Ansible  
- **Cloud Provider**: AWS (EC2)  
- **Operating System**: Ubuntu Server  
- **Application**: Python (sample web app)

---

## 🏗️ Architecture Overview

![Architecture Diagram](diagrams/architecture.png)

---

## 🔄 CI/CD Workflow

### 1️⃣ Continuous Integration (CI)

Triggered on every push to the `main` branch.

**CI pipeline tasks:**
- Checkout source code
- Setup application runtime environment
- Install dependencies
- Run application tests
- Build Docker image
- Push Docker image to Docker Hub

**Workflow file:**  
`.github/workflows/ci.yml`

✔ Ensures only tested and stable code proceeds to deployment.

---

### 2️⃣ Infrastructure Provisioning (Terraform)

Terraform is used to provision infrastructure on AWS in a fully automated and reproducible way.

**Terraform provisions:**
- EC2 instance (Ubuntu)
- Security Group (SSH + application port)
- Uses existing AWS Key Pair
- Outputs EC2 public IP

**Directory:**  
`terraform/`

**Commands used:**

terraform init
terraform plan
terraform apply

---

### 3️⃣ Continuous Deployment (CD) using Ansible

The CD pipeline is triggered automatically after CI completes successfully.

**CD pipeline tasks:**

- Checkout repository

- Install Ansible on GitHub runner

- Configure SSH using GitHub Secrets

- Run Ansible playbook to deploy application

**Workflow file:**
.github/workflows/cd.yml

---

### 4️⃣ Application Deployment on EC2

Ansible is responsible for configuring the EC2 instance and deploying the application.

**Ansible playbook tasks:**

- Install Docker on EC2

- Start Docker service

- Add user to Docker group

- Pull Docker image from Docker Hub

- Stop old container (if running)

- Run new application container

**Playbook file:**
ansible/deploy.yml

✔ Fully automated deployment
✔ No manual server intervention

📦 Application Deployment Flow
Developer pushes code to GitHub

CI pipeline runs tests and builds Docker image

Docker image is pushed to Docker Hub

CD pipeline triggers automatically

Ansible deploys the Docker container on EC2

Application becomes accessible via EC2 public IP

🔐 Security Best Practices
SSH private key stored securely in GitHub Secrets

Docker Hub credentials stored as GitHub Secrets

No secrets committed to the repository

Infrastructure managed using code (IaC)

📂 Repository Structure
.github/workflows/   # CI & CD pipelines
app/                # Application source code & Dockerfile
terraform/          # AWS infrastructure provisioning
ansible/            # Deployment automation
diagrams/           # Architecture diagram
README.md
✅ Key Learnings
Designing CI/CD pipelines end-to-end

Automating infrastructure with Terraform

Deploying containerized applications using Ansible

Secure secret handling in GitHub Actions

Debugging real-world CI/CD and deployment issues

📌 Future Enhancements
Add rollback strategy

Add monitoring and alerting

Introduce Load Balancer (ALB)

Add Docker image versioning

Migrate deployment to Kubernetes

👨‍💻 Author
Prasanna Pawar
Aspiring DevOps Engineer 🚀