# Spring Boot Application Deployment on Azure Kubernetes Service (AKS)

## Project Overview
This project demonstrates how to deploy a Spring Boot application on Azure Kubernetes Service (AKS) using Kubernetes deployment and service configuration.  
The application is containerized and deployed using a LoadBalancer service to expose it publicly.

This setup is beginner-friendly and reflects real-world production deployment patterns on Azure Cloud.

---

## Technologies Used
- Java Spring Boot
- Docker
- Kubernetes
- Azure Kubernetes Service (AKS)
- DockerHub Container Registry
- Azure CLI
- kubectl

---

## High-Level Architecture Diagram

    GitHub Repository
          |
          v
    DockerHub (Image Hosting)
          |
          v
    Azure Kubernetes Service (AKS)
          |
          v
     LoadBalancer Service
          |
          v
        Browser

---

## Step-by-Step Deployment Summary

### 1. Created Azure Kubernetes Cluster
- Created AKS cluster using Azure Portal
- Verified node health using kubectl

### 2. Created Kubernetes YAML Files
- deployment.yaml for application deployment
- service.yaml for exposing application

### 3. Updated Image Source
- Switched image from private ACR to public DockerHub image to avoid permission issue
- Updated Deployment YAML to use DockerHub image

### 4. Applied Kubernetes Configuration
- Uploaded and applied YAML via Azure Kubernetes UI
- Redeployed using kubectl when needed

### 5. Exposed Application
- Service type configured as LoadBalancer
- Azure automatically generated a public IP
- Accessed application in browser using external IP

---

## Kubernetes Configuration Files

### deployment.yaml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: springboot-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: springboot-app
  template:
    metadata:
      labels:
        app: springboot-app
    spec:
      containers:
      - name: springboot-app
        image: pankaj8900/springboot-app:latest
        imagePullPolicy: Always
        ports:
        - containerPort: 8080



### CLI
1.  az login

2. Connect kubectl to AKS cluster
az aks get-credentials --resource-group aks-demo-rg --name demo-aks-cluster

3. Check cluster health
kubectl get nodes

4. Deploy application
kubectl apply -f deployment.yaml
kubectl apply -f server.yaml

5. write a file
nano deployment.yaml

6 .check pods
kubectl get pods

7. get external Ip
kubectl get svc

8. Restart application deployments
kubectl delete pod -l app=springboot-app

9. http://<external-ip>/api/token




Author

Deployed by Pankaj Verma


## U done on these----
Azure Kubernetes Service Deployment
Spring Boot on Kubernetes
AKS Spring Boot Tutorial
DockerHub Kubernetes Deployment
Azure DevOps Kubernetes Setup
Microservices Deployment using AKS
