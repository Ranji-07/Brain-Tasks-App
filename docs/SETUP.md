# 📚 Setup & Configuration Guide

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Initialization](#initialization)
5. [Troubleshooting](#troubleshooting)

## Prerequisites

### Required Software
- **Terraform** 1.5.0 or higher
- **AWS CLI** 2.x or higher
- **Git** 2.0 or higher
- **Docker** 20.10+ (optional)
- **Bash** or equivalent shell

### AWS Prerequisites
- AWS Account with appropriate permissions
- IAM user with programmatic access
- AWS credentials configured locally

### System Requirements
- RAM: Minimum 2GB
- Disk Space: 1GB
- Internet Connection

## Installation

### Terraform Installation

#### macOS (Homebrew)
```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
terraform version
```

#### Ubuntu/Debian
```bash
curl https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
terraform version
```

#### Windows (Chocolatey)
```powershell
choco install terraform
terraform version
```

### AWS CLI Installation

```bash
# macOS
brew install awscli

# Linux
sudo apt-get install awscli

# Windows
choco install awscli

# Verify installation
aws --version
```

### Clone Repository

```bash
git clone https://github.com/Ranji-07/Brain-Tasks-App.git
cd Brain-Tasks-App
```

## Configuration

### AWS Credentials Setup

```bash
# Configure AWS CLI
aws configure

# You'll be prompted for:
# AWS Access Key ID: xxxxxx
# AWS Secret Access Key: xxxxxx
# Default region: us-east-1
# Default output format: json
```

### Environment Variables

```bash
# Set AWS region
export AWS_REGION=us-east-1

# Set environment
export TF_VAR_environment=dev

# Set project name
export TF_VAR_project_name=brain-tasks
```

### Terraform Variables

Create `terraform.tfvars`:

```hcl
# AWS Configuration
aws_region = "us-east-1"

# Project Configuration
project_name = "brain-tasks"
environment = "dev"

# VPC Configuration
vpc_cidr = "10.0.0.0/16"
availability_zones = ["us-east-1a", "us-east-1b"]

# Compute Configuration
instance_type = "t3.medium"
instance_count = 2

# Database Configuration
db_engine = "postgres"
db_instance_class = "db.t3.micro"
db_allocated_storage = 20
db_username = "admin"

# Tags
tags = {
  Environment = "dev"
  Project = "brain-tasks"
  ManagedBy = "terraform"
}
```

## Initialization

### Initialize Terraform

```bash
# Navigate to environment directory
cd environments/dev

# Initialize Terraform
terraform init

# Expected output:
# Terraform has been successfully configured for this workspace
```

### Validate Configuration

```bash
# Validate Terraform files
terraform validate

# Expected output:
# Success! The configuration is valid.
```

### Format Code

```bash
# Format all Terraform files
terraform fmt -recursive
```

### Generate Plan

```bash
# Create execution plan
terraform plan -out=tfplan

# Save plan to file
terraform plan -out=tfplan

# Review plan output before applying
```

## Verification Checklist

- [ ] Terraform installed: `terraform version`
- [ ] AWS CLI installed: `aws --version`
- [ ] AWS credentials configured: `aws sts get-caller-identity`
- [ ] Repository cloned
- [ ] `terraform.tfvars` created and configured
- [ ] Terraform initialized: `terraform init`
- [ ] Configuration validated: `terraform validate`
- [ ] Plan generated: `terraform plan`
- [ ] Ready for deployment

## Troubleshooting

### "Terraform command not found"
```bash
# Add to PATH if needed
echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc
source ~/.bashrc
terraform version
```

### "AWS credentials not found"
```bash
# Reconfigure AWS credentials
aws configure

# Or set environment variables
export AWS_ACCESS_KEY_ID=xxxxxx
export AWS_SECRET_ACCESS_KEY=xxxxxx
export AWS_DEFAULT_REGION=us-east-1
```

### "Backend configuration failed"
```bash
# Reinitialize backend
rm -rf .terraform
terraform init
```

For more issues, see [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
