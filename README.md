# DEVOPS-CORE-PROJECT
A complete CI/CD pipeline integrating Git → Jenkins → Docker → Kubernetes → AWS EC2 to automate build, deploy, and hosting of a static website.

##Project Architecture
Workflow:

Developer pushes code to GitHub

Jenkins pulls latest code via webhook

Jenkins builds Docker image

Docker image pushed to DockerHub

Kubernetes deployments apply the new image

Application accessible via EC2 public IP

##Tools & Technologies Used:

| Tool/Service | Purpose |
|--------------|---------|
| **Git & GitHub** | Version control + Webhook trigger |
| **Jenkins** | CI server for automated builds |
| **Docker** | Packaging application into containers |
| **DockerHub / ECR** | Hosting Docker images |
| **Kubernetes (k8s)** | Container orchestration |
| **AWS EC2** | Running Jenkins & Kubernetes cluster |
| **Nginx (inside container)** | Serving static website |

 ##Project Arc:
image>>>>>>>>>>>>



