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

### 1. 🖥️ Install Java

```bash
sudo apt update
sudo apt install openjdk-17-jre
```

### 2. 🖥️ Install Jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

### 3. 🖥️ Install Docker

```bash
sudo apt update
sudo apt install docker.io
```

### 4. 🖥️ Grant Jenkins user and Ubuntu user permission to docker deamon.

```bash
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
### 5. 🖥️ Install Sonarqube

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube
```

### 6. 🖥️ Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start --driver=docker --cpus=4 --memory=8192
```

### 7. 🖥️ Install kubectl

```bash
url -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### 8. 🖥️ Install Argo CD

```bash
url -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### 9. 🖥️ Install Prometheus Stack with Helm

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack \
  -n monitoring --create-namespace
```

## 🏗️ Project Architecture

The following diagram illustrates the complete CI/CD pipeline and deployment architecture used in this project:

![Architecture](./Jenkins_pipeline.png)
