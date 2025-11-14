.

🚀 DevOps CI/CD Pipeline — GitHub → Jenkins → DockerHub → Kubernetes (Minikube)

This project showcases a complete automated CI/CD pipeline that builds, containerizes, pushes, and deploys a static website using:

GitHub → Jenkins → Docker → DockerHub → Kubernetes (Minikube)

The website is built using Mobirise, packaged into an NGINX container, then deployed automatically.

📐 Architecture Overview

Developer pushes code to GitHub

Jenkins Pipeline triggers automatically

Jenkins performs:

Clone repository

Build Docker image

Push image to DockerHub

Kubernetes Deployment pulls the new image

NGINX (inside container) serves the static website

Website exposed using:

kubectl port-forward

or NodePort Service

🧩 Project Components
Frontend

Static site generated using Mobirise Portfolio Template.

Folder includes:

index.html

assets/

project.mobirise

🐳 Dockerfile
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html/
EXPOSE 80


This uses a lightweight NGINX image to serve all static files.

🔧 Jenkins Pipeline (Jenkinsfile)
pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('dockerhub-creds')
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/dhanushharsh/DEVOPS-CORE-PROJECT.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t harsh672/devops-project:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh '''
                    echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push harsh672/devops-project:latest'
            }
        }
    }
}

🐳 DockerHub Image

📦 Image: harsh672/devops-project:latest
Used directly by Kubernetes Deployment.

☸️ Kubernetes (Minikube) Deployment
1. Create Deployment
kubectl create deployment devops-website --image=harsh672/devops-project:latest

2. Expose via NodePort
kubectl expose deployment devops-website --type=NodePort --port=80

3. Get service URL
minikube service devops-website --url

4. Access from EC2 (with security group open)
http://<EC2-PUBLIC-IP>:<NodePort>

📸 Screenshots
✔ Jenkins Pipeline Success

✔ DockerHub Image

✔ Minikube Setup

✔ Live Website

✔ Website Pages






👤 Author

Harsh Saini

🔗 GitHub: https://github.com/dhanushharsh

🔗 LinkedIn: https://www.linkedin.com/in/harsh-saini-ab515628b/

🔗 Medium: https://medium.com/@mr.harshsaini108

📧 Email: mr.harshsaini108@gmail.com
