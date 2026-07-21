# Brain-Tasks-App - Infrastructure as Code

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Terraform](https://img.shields.io/badge/Terraform-1.5+-623CE4?style=for-the-badge&logo=terraform&logoColor=white)](https://www.terraform.io/)
[![HCL](https://img.shields.io/badge/HCL-90.2%-844FCC?style=for-the-badge&logo=hashicorp&logoColor=white)](https://www.terraform.io/language)
[![Docker](https://img.shields.io/badge/Docker-9.8%-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![AWS](https://img.shields.io/badge/AWS-Supported-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)](https://github.com/Ranji-07/Brain-Tasks-App)

> Infrastructure as Code (IaC) solution using Terraform and HCL for provisioning and managing cloud infrastructure. Automate your cloud deployments with Terraform configurations optimized for AWS, GCP, and Azure.

## 📋 Overview

**Brain-Tasks-App** is a comprehensive Infrastructure as Code project that provides reusable Terraform modules and configurations for cloud infrastructure automation. It demonstrates best practices for cloud provisioning, resource management, and infrastructure automation.

### Key Highlights
- 🏗️ **90.2% HCL** - Terraform configuration language
- 🐳 **9.8% Docker** - Container definitions
- ☁️ **Multi-Cloud** - AWS, GCP, Azure support
- 📦 **Modular Design** - Reusable infrastructure components
- 🔄 **CI/CD Ready** - Automated deployment pipelines
- 🛡️ **Security Focused** - Best practices implementation

## 🎯 Features

### Core Infrastructure
- ☁️ **Cloud Resources** - VPC, Subnets, Security Groups
- 💾 **Database Services** - RDS, DynamoDB, Managed Databases
- 🔐 **Security** - IAM roles, policies, encryption
- 🌐 **Networking** - Load balancers, CDN, DNS
- 📊 **Monitoring** - CloudWatch, metrics, alarms
- 🔄 **Auto-Scaling** - Dynamic resource scaling

### Terraform Modules
- VPC & Networking Module
- EC2 & Compute Module
- RDS Database Module
- S3 Storage Module
- Lambda Functions Module
- IAM & Security Module

## 📐 Tech Stack

| Component | Technology | Percentage |
|-----------|-----------|----------|
| **Infrastructure** | HCL (Terraform) | 90.2% |
| **Container Config** | Docker | 9.8% |
| **Cloud Platforms** | AWS, GCP, Azure | Multi-Cloud |
| **Version Control** | Git | Standard |
| **Automation** | Terraform, GitHub Actions | CI/CD |

## 🏗️ Project Structure

```
Brain-Tasks-App/
├── main.tf                      # Main Terraform configuration
├── variables.tf                 # Variable definitions
├── outputs.tf                   # Output values
├── terraform.tfvars             # Variable values
├── terraform.tfvars.example     # Example variables
├── backend.tf                   # Remote state configuration
├── provider.tf                  # Cloud provider setup
│
├── modules/                     # Reusable modules
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── locals.tf
│   ├── ec2/
│   ├── rds/
│   ├── s3/
│   ├── iam/
│   ├── lambda/
│   └── monitoring/
│
├── environments/                # Environment-specific configs
│   ├── dev/
│   │   ├── main.tf
│   │   ├── terraform.tfvars
│   │   └── backend.tf
│   ├── staging/
│   ├── prod/
│   └── dr/                      # Disaster Recovery
│
├── .github/
│   └── workflows/
│       ├── terraform-plan.yml
│       ├── terraform-apply.yml
│       └── terraform-validate.yml
│
├── docker/
│   ├── Dockerfile
│   ├── .dockerignore
│   └── docker-compose.yml
│
├── docs/
│   ├── SETUP.md
│   ├── ARCHITECTURE.md
│   ├── MODULES.md
│   ├── DEPLOYMENT.md
│   └── TROUBLESHOOTING.md
│
├── scripts/
│   ├── init.sh                  # Initialize Terraform
│   ├── plan.sh                  # Create plan
│   ├── apply.sh                 # Apply configuration
│   ├── destroy.sh               # Destroy resources
│   └── validate.sh              # Validate configuration
│
├── .gitignore
├── .terraformignore
├── Dockerfile
├── docker-compose.yml
├── Makefile
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── LICENSE
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- **Terraform**: 1.5 or higher
- **AWS CLI**: Latest version (for AWS deployments)
- **Docker**: 20.10+ (optional)
- **Git**: Latest version

### Installation

#### Install Terraform

**macOS**
```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

**Windows**
```powershell
choco install terraform
```

**Linux**
```bash
wget https://releases.hashicorp.com/terraform/1.5.0/terraform_1.5.0_linux_amd64.zip
unzip terraform_1.5.0_linux_amd64.zip
mv terraform /usr/local/bin/
```

### Setup Instructions

#### Step 1: Clone Repository
```bash
git clone https://github.com/Ranji-07/Brain-Tasks-App.git
cd Brain-Tasks-App
```

#### Step 2: Initialize Terraform
```bash
cd environments/dev
terraform init
```

#### Step 3: Configure AWS Credentials
```bash
aws configure
# Enter your AWS Access Key ID
# Enter your AWS Secret Access Key
# Enter default region (us-east-1)
# Enter default output format (json)
```

#### Step 4: Review Configuration
```bash
terraform plan
```

#### Step 5: Apply Configuration
```bash
terraform apply
```

### Using Docker

```bash
# Build Docker image
docker build -t brain-tasks-terraform:latest .

# Run with Docker Compose
docker-compose up

# Initialize Terraform in container
docker-compose run terraform init

# Plan deployment
docker-compose run terraform plan

# Apply configuration
docker-compose run terraform apply
```

## 📚 Available Modules

### VPC Module
```hcl
module "vpc" {
  source = "./modules/vpc"

  vpc_cidr = "10.0.0.0/16"
  environment = "dev"
  availability_zones = ["us-east-1a", "us-east-1b"]
}
```

### EC2 Module
```hcl
module "ec2" {
  source = "./modules/ec2"

  instance_type = "t3.medium"
  instance_count = 2
  vpc_id = module.vpc.vpc_id
  environment = "dev"
}
```

### RDS Module
```hcl
module "rds" {
  source = "./modules/rds"

  engine = "postgres"
  engine_version = "15.0"
  instance_class = "db.t3.micro"
  allocated_storage = 20
  environment = "dev"
}
```

## 🔄 Terraform Workflows

### Development Environment
```bash
cd environments/dev
terraform workspace select dev
terraform plan
terraform apply
```

### Staging Environment
```bash
cd environments/staging
terraform workspace select staging
terraform plan
terraform apply
```

### Production Environment
```bash
cd environments/prod
terraform workspace select prod
terraform plan
terraform apply -auto-approve=false
```

## 📊 Terraform Commands Reference

```bash
# Initialize working directory
terraform init

# Validate configuration
terraform validate

# Format code
terraform fmt -recursive

# Create execution plan
terraform plan -out=tfplan

# Apply configuration
terraform apply tfplan

# Show current state
terraform show

# List resources
terraform state list

# Show specific resource
terraform state show aws_instance.example

# Destroy resources
terraform destroy

# Refresh state
terraform refresh
```

## 🛡️ Best Practices

### Security
- ✅ **State Management** - Use remote state (Terraform Cloud, S3)
- ✅ **Encryption** - Enable encryption at rest and in transit
- ✅ **IAM Policies** - Follow principle of least privilege
- ✅ **Secrets Management** - Use AWS Secrets Manager or HashiCorp Vault
- ✅ **Auditing** - Enable CloudTrail and logging

### Infrastructure
- ✅ **Modularity** - Organize code into reusable modules
- ✅ **Variable Defaults** - Use sensible defaults
- ✅ **Tagging Strategy** - Tag all resources consistently
- ✅ **Documentation** - Document modules and variables
- ✅ **Testing** - Use Terratest for infrastructure testing

### CI/CD
- ✅ **Automated Validation** - Validate on every commit
- ✅ **Plan Reviews** - Review plans before apply
- ✅ **Environment Parity** - Keep environments consistent
- ✅ **Rollback Strategy** - Have rollback procedures
- ✅ **Version Control** - Version all infrastructure code

## 📖 Documentation

| Document | Purpose |
|----------|----------|
| [SETUP.md](./docs/SETUP.md) | Detailed setup instructions |
| [ARCHITECTURE.md](./docs/ARCHITECTURE.md) | Infrastructure architecture |
| [MODULES.md](./docs/MODULES.md) | Module documentation |
| [DEPLOYMENT.md](./docs/DEPLOYMENT.md) | Deployment procedures |
| [TROUBLESHOOTING.md](./docs/TROUBLESHOOTING.md) | Troubleshooting guide |

## 🔐 State Management

### Remote State Configuration

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"
  }
}
```

## 🚀 CI/CD Integration

### GitHub Actions Workflow

```yaml
name: Terraform

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: hashicorp/setup-terraform@v2
      - run: terraform init
      - run: terraform validate
      - run: terraform plan
```

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

### Development Workflow
1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m "feat: add amazing feature"`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 🐛 Reporting Issues

Found a bug? Open an [Issue](https://github.com/Ranji-07/Brain-Tasks-App/issues) with:
- Clear title and description
- Steps to reproduce
- Expected vs actual behavior
- Environment details (OS, Terraform version, AWS region)

## 📜 License

MIT License - see [LICENSE](./LICENSE) file for details.

## 🙏 Acknowledgments

- HashiCorp Terraform community
- AWS documentation and best practices
- Open-source contributors

## 📞 Support

- 📧 **Email**: [your-email@example.com](mailto:your-email@example.com)
- 🐛 **Issues**: [GitHub Issues](https://github.com/Ranji-07/Brain-Tasks-App/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/Ranji-07/Brain-Tasks-App/discussions)
- 📚 **Wiki**: [Project Wiki](https://github.com/Ranji-07/Brain-Tasks-App/wiki)

## 🔗 Related Resources

- [Terraform Documentation](https://www.terraform.io/docs/)
- [AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Terraform Best Practices](https://www.terraform.io/cloud-docs/recommended-practices)
- [Infrastructure as Code Guide](https://www.terraform.io/use-cases/infrastructure-as-code)

---

<div align="center">

**⭐ If you find this project helpful, please star the repository! ⭐**

[Back to top](#brain-tasks-app---infrastructure-as-code)

*Built with ❤️ by [Ranji-07](https://github.com/Ranji-07)*

</div>
