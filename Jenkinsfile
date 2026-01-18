pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        echo 'Building Docker images...'
        sh 'docker build -t frontend ./frontend'
        sh 'docker build -t backend ./backend'
      }
    }
    
    stage('Push to ACR') {
      steps {
        echo 'Pushing images to Azure Container Registry...'
        sh 'az acr login --name myacr123'
        sh 'docker tag frontend myacr123.azurecr.io/frontend:latest'
        sh 'docker tag backend myacr123.azurecr.io/backend:latest'
        sh 'docker push myacr123.azurecr.io/frontend:latest'
        sh 'docker push myacr123.azurecr.io/backend:latest'
      }
    }
    
    stage('Deploy to AKS') {
      steps {
        echo 'Deploying to Azure Kubernetes Service...'
        sh 'kubectl apply -f k8s/'
        sh 'kubectl get svc'
      }
    }
  }
  
  post {
    success {
      echo 'Pipeline executed successfully!'
    }
    failure {
      echo 'Pipeline failed!'
    }
  }
}
