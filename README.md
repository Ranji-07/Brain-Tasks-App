# Brain-Tasks-App - DevOps & AWS Infrastructure Practice Project

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Terraform](https://img.shields.io/badge/Terraform-1.5+-623CE4?style=for-the-badge&logo=terraform&logoColor=white)](https://www.terraform.io/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![CodePipeline](https://img.shields.io/badge/CodePipeline-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/codepipeline/)
[![DevOps](https://img.shields.io/badge/DevOps-Practice-blueviolet?style=for-the-badge)](https://github.com/Ranji-07/Brain-Tasks-App)

> 🎓 **Comprehensive DevOps & AWS Infrastructure Practice Project** - Master container orchestration, Kubernetes, AWS services, and enterprise-grade CI/CD pipelines through hands-on implementation.

## 🎯 Project Overview

This is a **comprehensive DevOps practice project** designed to master containerization, Kubernetes, and AWS services. It implements:

- 🐳 **Docker containerization** with Dockerfile optimization
- 📦 **AWS ECR registry** for private image storage
- ☸️ **Kubernetes (EKS)** setup and deployment
- 🔄 **AWS CodeBuild** for automated builds
- 🚀 **AWS CodePipeline** for CI/CD orchestration
- 📊 **CloudWatch monitoring** and logging
- 🏗️ **Terraform** for Infrastructure as Code
- 🔐 **Security best practices** implementation

## 📚 Learning Objectives

This project helps you practice:

### Docker & Containerization
- ✅ Dockerfile creation and optimization
- ✅ Image best practices (layer caching, size optimization)
- ✅ Container security scanning
- ✅ Multi-stage builds
- ✅ Docker networking and volumes

### AWS ECR Registry
- ✅ AWS Elastic Container Registry setup
- ✅ Image repository management
- ✅ Access control and permissions
- ✅ Image lifecycle policies
- ✅ Registry authentication

### Kubernetes (EKS)
- ✅ AWS EKS cluster creation
- ✅ Node group management
- ✅ Deployment and Service manifests
- ✅ ConfigMaps and Secrets
- ✅ Horizontal Pod Autoscaling (HPA)
- ✅ Ingress configuration
- ✅ Helm charts (optional)

### AWS CodeBuild
- ✅ CodeBuild project configuration
- ✅ buildspec.yml creation
- ✅ Build environment setup
- ✅ Artifact management
- ✅ Build caching strategies
- ✅ Environment variables and secrets

### AWS CodePipeline
- ✅ Pipeline orchestration
- ✅ Multi-stage deployments
- ✅ Approval gates
- ✅ Cross-region deployments
- ✅ Pipeline monitoring
- ✅ Error handling and rollbacks

### CloudWatch Monitoring
- ✅ Log group and stream creation
- ✅ Log retention policies
- ✅ Metric dashboards
- ✅ Alarms and notifications
- ✅ Log insights queries
- ✅ Application performance monitoring

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|----------|
| **Infrastructure** | Terraform + HCL | IaC |
| **Containerization** | Docker | Application packaging |
| **Container Registry** | AWS ECR | Image storage |
| **Orchestration** | Kubernetes (EKS) | Container management |
| **Build Automation** | AWS CodeBuild | Build pipeline |
| **CI/CD** | AWS CodePipeline | Orchestration |
| **Monitoring** | CloudWatch | Logging & metrics |
| **Cloud Platform** | AWS | Cloud infrastructure |

## 🏗️ Project Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                 Git Repository                                │
│              (Development & Production)                       │
└────────────────────┬─────────────────────────────────────────┘
                     │
                     ▼ (Webhook Trigger)
        ┌────────────────────────────┐
        │   AWS CodePipeline         │
        │  ┌──────────────────────┐  │
        │  │ Source: GitHub       │  │
        │  │ Build: CodeBuild     │  │
        │  │ Deploy: EKS          │  │
        │  └──────────────────────┘  │
        └───────────┬────────────────┘
                    │
         ┌──────────┴──────────┐
         │                     │
         ▼                     ▼
    ┌─────────────┐      ┌──────────────┐
    │ AWS CodeBuild          │ AWS CodeBuild
    │ (Build Job)    │      │ (Build Job)  │
    └─────────────┘      └──────────────┘
         │                     │
         ▼                     ▼
    ┌─────────────┐      ┌──────────────┐
    │  AWS ECR    │      │   AWS ECR    │
    │ (dev images)│      │(prod images) │
    └─────────────┘      └──────────────┘
         │                     │
         └──────────┬──────────┘
                    │
                    ▼
        ┌────────────────────────────┐
        │   AWS EKS Cluster          │
        │  ┌──────────────────────┐  │
        │  │ Deployment           │  │
        │  │ Service              │  │
        │  │ ConfigMaps/Secrets   │  │
        │  │ HPA                  │  │
        │  └──────────────────────┘  │
        └───────────┬────────────────┘
                    │
                    ▼
        ┌────────────────────────────┐
        │   CloudWatch Monitoring    │
        │  - Logs & Metrics          │
        │  - Alarms & Alerts         │
        │  - Dashboards              │
        └────────────────────────────┘
```

## 📋 Implementation Checklist

### Docker Implementation ✅
- [x] **Dockerfile Creation**
  ```dockerfile
  FROM node:18-alpine AS builder
  WORKDIR /app
  COPY package*.json ./
  RUN npm ci
  COPY . .
  RUN npm run build
  
  FROM node:18-alpine
  WORKDIR /app
  COPY --from=builder /app/node_modules ./
  COPY --from=builder /app/dist ./dist
  EXPOSE 3000
  CMD ["node", "dist/server.js"]
  ```
- [x] **Build and Test**
  ```bash
  docker build -t app:latest .
  docker run -p 3000:3000 app:latest
  # Verify at http://localhost:3000
  ```

### AWS ECR Registry ✅
- [x] **ECR Repository Setup**
  ```bash
  aws ecr create-repository --repository-name app-dev
  aws ecr create-repository --repository-name app-prod
  ```
- [x] **Image Tagging & Pushing**
  ```bash
  aws ecr get-login-password --region us-east-1 | \
    docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
  
  docker tag app:latest <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/app-dev:latest
  docker push <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/app-dev:latest
  ```

### Kubernetes (EKS) ✅
- [x] **EKS Cluster Setup**
  ```bash
  aws eks create-cluster \
    --name app-cluster \
    --version 1.27 \
    --role-arn arn:aws:iam::ACCOUNT:role/eks-service-role \
    --resources-vpc-config subnetIds=subnet-1,subnet-2
  
  # Verify cluster
  aws eks describe-cluster --name app-cluster
  ```
- [x] **kubectl Configuration**
  ```bash
  aws eks update-kubeconfig --name app-cluster --region us-east-1
  kubectl get nodes
  ```
- [x] **Deployment Manifest** (deployment.yaml)
  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: app-deployment
  spec:
    replicas: 3
    selector:
      matchLabels:
        app: app
    template:
      metadata:
        labels:
          app: app
      spec:
        containers:
        - name: app
          image: <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/app:latest
          ports:
          - containerPort: 3000
          resources:
            requests:
              memory: "256Mi"
              cpu: "100m"
  ```
- [x] **Service Manifest** (service.yaml)
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: app-service
  spec:
    type: LoadBalancer
    selector:
      app: app
    ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  ```
- [x] **Deploy to EKS**
  ```bash
  kubectl apply -f deployment.yaml
  kubectl apply -f service.yaml
  kubectl get pods
  kubectl get svc
  ```

### AWS CodeBuild ✅
- [x] **CodeBuild Project Creation**
  ```bash
  aws codebuild create-project \
    --name app-build \
    --source type=GITHUB,location=https://github.com/Ranji-07/repo.git \
    --environment computeType=BUILD_GENERAL1_SMALL,image=aws/codebuild/standard:5.0,type=LINUX_CONTAINER \
    --service-role arn:aws:iam::ACCOUNT:role/codebuild-role
  ```
- [x] **buildspec.yml Configuration**
  ```yaml
  version: 0.2
  phases:
    pre_build:
      commands:
        - echo "Building the Docker image..."
        - aws ecr get-login-password | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com
        - REPOSITORY_URI=$AWS_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/app
        - COMMIT_HASH=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)
        - IMAGE_TAG=${COMMIT_HASH:=latest}
    build:
      commands:
        - docker build -t $REPOSITORY_URI:$IMAGE_TAG .
        - docker push $REPOSITORY_URI:$IMAGE_TAG
    post_build:
      commands:
        - echo "Build completed"
        - printf '[{"name":"app","imageUri":"%s"}]' $REPOSITORY_URI:$IMAGE_TAG > imagedefinitions.json
  artifacts:
    files: imagedefinitions.json
  ```

### AWS CodePipeline ✅
- [x] **Pipeline Configuration**
  ```bash
  aws codepipeline create-pipeline \
    --cli-input-json file://pipeline.json
  ```
- [x] **Pipeline Stages**
  ```json
  {
    "stages": [
      {
        "name": "Source",
        "actions": [
          {
            "name": "SourceAction",
            "actionTypeId": {
              "category": "Source",
              "owner": "ThirdParty",
              "provider": "GitHub",
              "version": "1"
            }
          }
        ]
      },
      {
        "name": "Build",
        "actions": [
          {
            "name": "BuildAction",
            "actionTypeId": {
              "category": "Build",
              "owner": "AWS",
              "provider": "CodeBuild",
              "version": "1"
            }
          }
        ]
      },
      {
        "name": "Deploy",
        "actions": [
          {
            "name": "DeployAction",
            "actionTypeId": {
              "category": "Deploy",
              "owner": "AWS",
              "provider": "AppConfig",
              "version": "1"
            }
          }
        ]
      }
    ]
  }
  ```

### CloudWatch Monitoring ✅
- [x] **Log Group & Streams**
  ```bash
  aws logs create-log-group --log-group-name /aws/eks/app
  aws logs create-log-stream --log-group-name /aws/eks/app --log-stream-name app-logs
  ```
- [x] **Metrics & Alarms**
  ```bash
  aws cloudwatch put-metric-alarm \
    --alarm-name app-cpu-high \
    --alarm-description "Alert if CPU usage is high" \
    --metric-name CPUUtilization \
    --namespace AWS/ECS \
    --statistic Average \
    --period 300 \
    --threshold 80 \
    --comparison-operator GreaterThanThreshold
  ```
- [x] **Dashboards**
  ```bash
  aws cloudwatch put-dashboard \
    --dashboard-name app-dashboard \
    --dashboard-body file://dashboard.json
  ```
- [x] **SNS Notifications**
  ```bash
  aws sns subscribe \
    --topic-arn arn:aws:sns:us-east-1:ACCOUNT:app-alerts \
    --protocol email \
    --notification-endpoint your-email@example.com
  ```

### Terraform Infrastructure ✅
- [x] **VPC & Networking** (modules/vpc)
- [x] **EKS Cluster** (modules/eks)
- [x] **ECR Repositories** (modules/ecr)
- [x] **Security Groups** (modules/security)
- [x] **CloudWatch** (modules/monitoring)

## 📂 Repository Structure

```
Brain-Tasks-App/
├── main.tf                         # Root Terraform config
├── variables.tf                    # Input variables
├── outputs.tf                      # Outputs
├── backend.tf                      # Remote state config
├── provider.tf                     # Cloud provider setup
│
├── modules/
│   ├── vpc/                       # Networking module
│   ├── eks/                       # Kubernetes cluster
│   ├── ecr/                       # Container registry
│   ├── codebuild/                 # Build pipeline
│   ├── codepipeline/              # CI/CD orchestration
│   ├── security/                  # Security groups
│   └── monitoring/                # CloudWatch setup
│
├── environments/
│   ├── dev/
│   │   ├── terraform.tfvars       # Dev settings
│   │   └── main.tf                # Dev resources
│   ├── staging/
│   └── prod/
│
├── kubernetes/
│   ├── deployment.yaml            # Deployment manifest
│   ├── service.yaml               # Service manifest
│   ├── configmap.yaml             # ConfigMaps
│   ├── secret.yaml                # Secrets
│   ├── hpa.yaml                   # Auto-scaling
│   └── ingress.yaml               # Ingress config
│
├── docker/
│   ├── Dockerfile
│   └── .dockerignore
│
├── buildspec.yml                  # CodeBuild config
├── pipeline.json                  # CodePipeline config
│
├── scripts/
│   ├── create-cluster.sh          # EKS cluster setup
│   ├── deploy.sh                  # Kubernetes deployment
│   ├── monitoring-setup.sh        # CloudWatch setup
│   └── cleanup.sh                 # Resource cleanup
│
├── docs/
│   ├── SETUP.md                   # Terraform setup
│   ├── ARCHITECTURE.md            # Architecture overview
│   ├── AWS_CODEBUILD.md           # CodeBuild guide
│   ├── AWS_CODEPIPELINE.md        # CodePipeline guide
│   ├── EKS_DEPLOYMENT.md          # EKS deployment
│   └── MONITORING.md              # Monitoring setup
│
└── README.md
```

## 🚀 Quick Start

### Prerequisites
```bash
# Install AWS CLI
aws --version

# Install Terraform
terraform version

# Install kubectl
kubectl version --client

# Install Docker
docker version
```

### Deploy Infrastructure

```bash
# Initialize Terraform
cd environments/dev
terraform init

# Plan deployment
terraform plan

# Apply configuration
terraform apply
```

### Deploy Application

```bash
# Get EKS credentials
aws eks update-kubeconfig --name app-cluster

# Deploy to Kubernetes
kubectl apply -f ../../kubernetes/

# Verify deployment
kubectl get pods
kubectl get svc
```

## 📚 Documentation

| Guide | Purpose |
|-------|----------|
| [SETUP.md](./docs/SETUP.md) | Terraform & infrastructure setup |
| [ARCHITECTURE.md](./docs/ARCHITECTURE.md) | System architecture & design |
| [AWS_CODEBUILD.md](./docs/AWS_CODEBUILD.md) | CodeBuild configuration |
| [AWS_CODEPIPELINE.md](./docs/AWS_CODEPIPELINE.md) | CodePipeline setup |
| [EKS_DEPLOYMENT.md](./docs/EKS_DEPLOYMENT.md) | Kubernetes deployment |
| [MONITORING.md](./docs/MONITORING.md) | CloudWatch monitoring |

## 🎓 Learning Resources

### AWS Services
- [AWS EKS Documentation](https://docs.aws.amazon.com/eks/)
- [AWS CodeBuild Guide](https://docs.aws.amazon.com/codebuild/)
- [AWS CodePipeline Documentation](https://docs.aws.amazon.com/codepipeline/)
- [CloudWatch User Guide](https://docs.aws.amazon.com/cloudwatch/)

### Kubernetes
- [Kubernetes Official Docs](https://kubernetes.io/docs/)
- [Kubernetes Best Practices](https://kubernetes.io/docs/concepts/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

### Terraform
- [Terraform Documentation](https://www.terraform.io/docs/)
- [AWS Provider Reference](https://registry.terraform.io/providers/hashicorp/aws/latest)

## 💡 Key Learnings

### Container Orchestration
- ✅ Kubernetes cluster management
- ✅ Pod lifecycle and scheduling
- ✅ Service discovery and load balancing
- ✅ Persistent storage management
- ✅ Network policies and security

### CI/CD Practices
- ✅ Automated build pipelines
- ✅ Continuous deployment strategies
- ✅ Blue-green deployments
- ✅ Canary releases
- ✅ Rollback procedures

### Infrastructure as Code
- ✅ Terraform best practices
- ✅ Module composition
- ✅ State management
- ✅ Environment parity
- ✅ Version control for infrastructure

### Monitoring & Observability
- ✅ Application performance monitoring
- ✅ Infrastructure metrics
- ✅ Log aggregation and analysis
- ✅ Alert configuration
- ✅ Incident response

## 🤝 Contributing

This is a practice project. Feel free to:
- Fork and experiment
- Improve automation
- Add new AWS services
- Share learnings

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## 📞 Support

- 📧 **Email**: [your-email@example.com](mailto:your-email@example.com)
- 🐛 **Issues**: [GitHub Issues](https://github.com/Ranji-07/Brain-Tasks-App/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/Ranji-07/Brain-Tasks-App/discussions)

## 📜 License

MIT License - see [LICENSE](./LICENSE) file for details.

---

<div align="center">

**🎓 This is a DevOps & AWS Infrastructure Practice Project**

*Master Kubernetes, CI/CD, and cloud infrastructure through hands-on implementation*

[Back to top](#brain-tasks-app---devops--aws-infrastructure-practice-project)

*Built with ❤️ by [Ranji-07](https://github.com/Ranji-07)*

</div>
