# 🚀 Cloud-Native Web App Deployment

**Azure | Docker | Jenkins | Kubernetes (AKS)**

## 📌 Overview

This repository demonstrates a **complete DevOps pipeline** to build, containerize, automate, and deploy a **modern web application** on **Microsoft Azure** using industry-standard tools.

The project is designed for:

- **Portfolio / Resume**
- **DevOps Interviews**
- **Real-world learning**

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React (Modern UI) |
| Backend | Node.js + Express |
| Containers | Docker |
| CI/CD | Jenkins |
| Orchestration | Kubernetes |
| Cloud | Azure (AKS + ACR) |
| Hosting | Azure LoadBalancer |

## 🏗️ Architecture

```
User → Azure Load Balancer → Kubernetes (AKS)
        ├── Frontend Pods (React)
        └── Backend Pods (Node.js API)
```

## 📂 Repository Structure

```
cloud-native-web-app/
│
├── frontend/
│   ├── Dockerfile
│   └── src/
│
├── backend/
│   ├── Dockerfile
│   └── server.js
│
├── k8s/
│   ├── frontend-deployment.yaml
│   ├── backend-deployment.yaml
│   └── service.yaml
│
├── Jenkinsfile
├── docker-compose.yml
└── README.md
```

## ⚙️ Prerequisites

- Azure Account
- Docker
- Jenkins
- kubectl
- Azure CLI
- Git

## 🚀 Setup & Deployment Steps

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-username/cloud-native-web-app.git
cd cloud-native-web-app
```

### 2️⃣ Build the Web Application

#### Frontend

```bash
cd frontend
npm install
npm start
```

#### Backend

```bash
cd backend
npm install
node server.js
```

### 3️⃣ Dockerize the Application

#### Frontend Dockerfile

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install && npm run build
EXPOSE 3000
CMD ["npm","start"]
```

#### Backend Dockerfile

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 5000
CMD ["node","server.js"]
```

### 4️⃣ Push Images to Azure Container Registry (ACR)

```bash
az group create --name devops-rg --location eastus
az acr create --resource-group devops-rg --name myacr123 --sku Basic
az acr login --name myacr123
```

```bash
docker tag frontend myacr123.azurecr.io/frontend:latest
docker tag backend myacr123.azurecr.io/backend:latest
docker push myacr123.azurecr.io/frontend:latest
docker push myacr123.azurecr.io/backend:latest
```

### 5️⃣ Create Kubernetes Cluster (AKS)

```bash
az aks create \
  --resource-group devops-rg \
  --name devops-cluster \
  --node-count 2 \
  --generate-ssh-keys
```

```bash
az aks get-credentials --resource-group devops-rg --name devops-cluster
```

### 6️⃣ Deploy to Kubernetes

```bash
kubectl apply -f k8s/
kubectl get svc
```

Access the application using the **EXTERNAL-IP**.

## 🔄 Jenkins CI/CD Pipeline

The Jenkins pipeline automates:

1. Docker image build
2. Push to Azure Container Registry
3. Deploy to AKS

### Jenkinsfile

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t frontend ./frontend'
        sh 'docker build -t backend ./backend'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push myacr123.azurecr.io/frontend:latest'
        sh 'docker push myacr123.azurecr.io/backend:latest'
      }
    }
    stage('Deploy') {
      steps {
        sh 'kubectl apply -f k8s/'
      }
    }
  }
}
```

## 🌐 Live Hosting

The application is hosted on **Azure Kubernetes Service** and exposed using an **Azure LoadBalancer**.

## 🔐 Best Practices Implemented

- ✅ Containerized microservices
- ✅ CI/CD automation
- ✅ Scalable Kubernetes deployments
- ✅ Cloud-native architecture
- ✅ Infrastructure as Code
- ✅ DevOps best practices

## 📈 Future Improvements

- Ingress Controller + HTTPS
- Helm charts
- Auto-scaling (HPA)
- Azure Monitor & Logs
- Authentication (JWT / Azure AD)
- Blue-Green deployments

## 👨‍💻 Author

**Dhanush S M**

Aspiring Cloud & DevOps Engineer

📍 Bengaluru, India

## ⭐ Contributing

Feel free to fork, modify, and submit pull requests. Contributions are welcome!

## 📝 License

MIT License - feel free to use this project for personal and professional purposes.

---

**🔥 Want to use this for your portfolio?**

I can help you with:

- Adding architecture diagrams
- Making it resume-optimized
- Adding screenshots & demo UI
- Converting it into a production-grade repo

Just reach out! 🚀
