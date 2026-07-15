# Brain Tasks App - End-to-End DevOps Project

## Project Overview

This project demonstrates an end-to-end DevOps CI/CD pipeline using AWS services. The application is containerized with Docker, stored in Amazon ECR, deployed to Amazon EKS, automated with AWS CodeBuild and CodePipeline, and monitored using Amazon CloudWatch.

---

## Repository Structure

Your final repository should look like this:

```text
Brain-Tasks-App/
│
├── dist/
├── Dockerfile
├── nginx.conf
├── deployment.yaml
├── service.yaml
├── buildspec.yml
├── terraform/
│   ├── provider.tf
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
│
├── screenshots/
│   ├── 01-local-app.png
│   ├── 02-docker-build.png
│   ├── 03-ecr.png
│   ├── 04-eks-cluster.png
│   ├── 05-kubectl-pods.png
│   ├── 06-loadbalancer.png
│   ├── 07-codebuild.png
│   ├── 08-codepipeline.png
│   ├── 09-cloudwatch.png
│   └── 10-final-output.png
│
└── README.md
```

---

## Architecture

```text
Developer
    │
    ▼
 GitHub Repository
    │
    ▼
AWS CodePipeline
    │
    ▼
AWS CodeBuild
    │
    ▼
Docker Build
    │
    ▼
Amazon ECR
    │
    ▼
Amazon EKS
    │
    ▼
Kubernetes Deployment
    │
    ▼
LoadBalancer
    │
    ▼
Application
```

---

## Technologies Used

- AWS
- Docker
- Amazon ECR
- Amazon EKS
- Kubernetes
- AWS CodeBuild
- AWS CodePipeline
- Amazon CloudWatch
- Terraform
- Git
- GitHub
- Nginx

---

## Prerequisites

- AWS Account
- IAM User
- AWS CLI
- kubectl
- Docker Desktop
- Terraform
- Git

---

## Project Structure

```text
Brain-Tasks-App/
├── dist/
├── Dockerfile
├── nginx.conf
├── deployment.yaml
├── service.yaml
├── buildspec.yml
├── terraform/
└── README.md
```

---

## Clone Repository

```bash
git clone https://github.com/<your-github-username>/Brain-Tasks-App.git
cd Brain-Tasks-App
```

---

## Docker Build

```bash
docker build -t brain-tasks-app:v1 .
```

Run container:

```bash
docker run -d -p 3000:3000 --name brain-app brain-tasks-app:v1
```

Verify:

```bash
docker ps
```

---

## Push Image to Amazon ECR

Login:

```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <account-id>.dkr.ecr.<region>.amazonaws.com
```

Tag:

```bash
docker tag brain-tasks-app:v1 <account-id>.dkr.ecr.<region>.amazonaws.com/brain-tasks-app:v1
```

Push:

```bash
docker push <account-id>.dkr.ecr.<region>.amazonaws.com/brain-tasks-app:v1
```

---

## Deploy to Amazon EKS

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
```

---

## CI/CD Pipeline

GitHub → CodePipeline → CodeBuild → Amazon ECR → Amazon EKS

---

## Monitoring

Amazon CloudWatch Logs is used for:

- CodeBuild logs
- Kubernetes control plane logs
- Application logs

---

## Verification Commands

```bash
kubectl get nodes
kubectl get pods
kubectl get svc
docker images
docker ps
aws ecr describe-repositories
```

---

## Troubleshooting

### ImagePullBackOff

Check image name and ECR permissions.

### CrashLoopBackOff

Check application logs:

```bash
kubectl logs <pod-name>
```

### LoadBalancer Pending

Ensure worker nodes are running and subnets are configured correctly.

---

## Future Enhancements

- Helm Charts
- GitOps using ArgoCD
- Prometheus & Grafana Monitoring
- Horizontal Pod Autoscaler
- AWS WAF
- HTTPS using ACM

---

## Screenshots

Add the following screenshots:

- GitHub Repository
- Docker Build
- Docker Container
- Amazon ECR
- Amazon EKS
- Kubernetes Pods
- Kubernetes Services
- LoadBalancer
- CodeBuild
- CodePipeline
- CloudWatch
- Final Application Output

---

## Author

Your Name

GitHub: https://github.com/Ranji-07
