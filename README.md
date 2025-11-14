<p align="center">
  <img src="https://img.shields.io/badge/DevOps-CI%2FCD%20Pipeline-blue?style=for-the-badge&logo=devops" />
  <img src="https://img.shields.io/badge/Docker-Containerization-brightgreen?style=for-the-badge&logo=docker" />
  <img src="https://img.shields.io/badge/Kubernetes-Orchestration-blue?style=for-the-badge&logo=kubernetes" />
  <img src="https://img.shields.io/badge/Jenkins-Automation-red?style=for-the-badge&logo=jenkins" />
</p>

<h1 align="center">🚀 DevOps CI/CD Pipeline — GitHub → Jenkins → DockerHub → Kubernetes</h1>








#DevOps CI/CD Pipeline — GitHub → Jenkins → DockerHub → Kubernetes#

This project demonstrates a complete DevOps pipeline using **GitHub**, **Jenkins**, **Docker**, **DockerHub**, and **Kubernetes (Minikube)**.  
The goal is to automate build, containerization, image publishing, and deployment of a static website created with **Mobirise**.



##Architecture Overview

1. **Developer pushes code to GitHub**
2. **Jenkins Pipeline triggers automatically**
3. Jenkins:
   - Clones repository  
   - Builds Docker image  
   - Pushes image to DockerHub  
4. **Kubernetes Deployment** pulls the new Docker image
5. NGINX inside the container serves the website
6. The site is exposed through Kubernetes using port-forward or NodePort


##Project Components

### **Frontend**
- Static website created using Mobirise Portfolio Template  
- Files included:
  - `index.html`
  - `assets/`
  - `project.mobirise`

### **Dockerfile**
Uses lightweight NGINX to serve the site:

```dockerfile
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html/
EXPOSE 80


### **Jenkinsfile**

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


### *Dockerhub* image ###
at -- harsh672/devops-project:latest

then ---
## K8S *MINIKUBE* ##
1. Create Deployment         2. Expose Service (NodePort)       3. Using Kubernetes port-forward           4. http://<EC2-PUBLIC-IP>:port


## screenshots

### ✔ Jenkins Pipeline Success
![Pipeline Success](./screenshots/jenkins-success-1.PNG)

![Pipeline Logs](./screenshots/jenkins-success-2.PNG)

### ✔ DockerHub Image
![DockerHub Image](./screenshots/dockerhub-image.PNG)

### ✔ Minikube Setup
![Minikube Setup](./screenshots/minikube-setup.PNG)

### ✔ Live Website
![Live Website](./screenshots/website-live-1.PNG)

### ✔ Website Pages
![Home Page](./screenshots/website-page2.PNG)
![Tools Page](./screenshots/website-page3.PNG)
![Process Page](./screenshots/website-page4.PNG)





### Author ###

**Harsh Saini**  
🔗 GitHub: https://github.com/dhanushharsh  
🔗 LinkedIn: https://www.linkedin.com/in/harsh-saini-ab515628b/  
🔗 Medium: https://medium.com/@mr.harshsaini108  
📧 Email: mr.harshsaini108@gmail.com



