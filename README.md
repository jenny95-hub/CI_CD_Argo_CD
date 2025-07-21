# CI_CD_Argo_CD
# 🚀 DevOps CI/CD Pipeline with Jenkins | Docker | SonarQube | Argo CD | Spring Boot | Prometheus | Grafana

This project demonstrates a complete CI/CD pipeline for deploying a Spring Boot application using Jenkins, Docker, SonarQube, Argo CD, and Kubernetes (via Minikube on EC2). It also includes observability using Prometheus and Grafana.

---

## 🛠️ Project Components

### 🔧 CI/CD Stack
- **Jenkins** – Automates the build, test, and deploy process.
- **Docker** – Containerizes the Spring Boot application.
- **SonarQube** – Performs static code analysis.
- **Argo CD** – GitOps deployment to Kubernetes.

### 📈 Monitoring & Observability
- **Prometheus** – Collects metrics from Kubernetes nodes and pods.
- **Grafana** – Visualizes metrics and cluster health.

### ☁️ Infrastructure
- **EC2 (Ubuntu)** – Single VM host for all DevOps tools.
- **Minikube** – Local Kubernetes cluster (installed on EC2).

---
## 🔁 Pipeline Workflow

### 1. **Developer pushes code to GitHub**
- Jenkins pipeline is triggered manually by the user from the Jenkins dashboard.

(Webhooks or Git polling can be configured later for full automation.)

### 2. **Jenkins executes the pipeline:**
- **Clones repo**
- **Runs SonarQube analysis**
- **Builds Docker image**
- **Pushes image to Docker Hub**
- **Updates Kubernetes manifest in Git**
- **Argo CD pulls and deploys it**

### 3. **Argo CD**
- Monitors Git for changes.
- Applies updated manifests to Minikube.

### 4. **Prometheus & Grafana**
- Monitor pods, containers, and system metrics.

---

## ✅ Prerequisites

- EC2 instance (t2.large or higher recommended)
- Ubuntu 20.04+ installed
- Docker & Minikube installed
- Jenkins, SonarQube, and Argo CD installed on EC2
- Internet access to pull Docker images and git repositories

---

## ⚙️ Setup Instructions

### 1. 🖥️ Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start --driver=docker --cpus=4 --memory=8192
