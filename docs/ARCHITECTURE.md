# 🏗️ Infrastructure Architecture

## System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Internet (Users)                        │
└─────────────────────────────┬───────────────────────────────┘
                              │
                    ┌─────────▼──────────┐
                    │   AWS Route 53     │
                    │     (DNS)          │
                    └─────────┬──────────┘
                              │
                ┌─────────────▼──────────────┐
                │   CloudFront (CDN)        │
                │   Content Delivery        │
                └─────────────┬──────────────┘
                              │
              ┌───────────────┴──────────────┐
              │                              │
        ┌─────▼──────────┐          ┌────────▼──────┐
        │ Application   │          │   Static      │
        │ Load Balancer  │          │   Content     │
        │ (ALB)          │          │   (S3)        │
        └─────┬──────────┘          └───────────────┘
              │
        ┌─────▼──────────────────────────┐
        │        VPC (10.0.0.0/16)       │
        │                                │
        │  ┌─────────┬─────────┐        │
        │  │ AZ-1a   │ AZ-1b   │        │
        │  │         │         │        │
        │  │ ┌─────┐ │ ┌─────┐ │        │
        │  │ │ App │ │ │ App │ │        │
        │  │ │ EC2 │ │ │ EC2 │ │        │
        │  │ └─────┘ │ └─────┘ │        │
        │  │         │         │        │
        │  └─────────┴─────────┘        │
        │                                │
        │  ┌──────────────────────┐      │
        │  │    RDS Cluster       │      │
        │  │    PostgreSQL        │      │
        │  │  Multi-AZ HA         │      │
        │  └──────────────────────┘      │
        │                                │
        └────────────────────────────────┘
```

## Terraform Module Architecture

```
Root Module (main.tf)
    │
    ├── VPC Module
    │   ├── VPC
    │   ├── Subnets (Public/Private)
    │   ├── NAT Gateways
    │   ├── Internet Gateway
    │   └── Route Tables
    │
    ├── EC2 Module
    │   ├── Security Groups
    │   ├── Launch Templates
    │   ├── Auto Scaling Groups
    │   └── Instances
    │
    ├── RDS Module
    │   ├── DB Subnet Group
    │   ├── DB Instance
    │   ├── DB Parameter Group
    │   └── Backups
    │
    ├── S3 Module
    │   ├── Buckets
    │   ├── Versioning
    │   └── Access Controls
    │
    ├── IAM Module
    │   ├── Roles
    │   ├── Policies
    │   └── Users
    │
    ├── Lambda Module
    │   ├── Functions
    │   └── Triggers
    │
    └── Monitoring Module
        ├── CloudWatch Alarms
        ├── Metrics
        └── Logging
```

## Environment Separation

```
Environments/
├── dev/
│   ├── terraform.tfvars (dev settings)
│   └── main.tf (dev references)
│
├── staging/
│   ├── terraform.tfvars (staging settings)
│   └── main.tf (staging references)
│
└── prod/
    ├── terraform.tfvars (prod settings)
    └── main.tf (prod references)
```

## Data Flow

1. **DNS Request** → Route 53
2. **Content Delivery** → CloudFront (CDN)
3. **Load Balancing** → ALB
4. **Application** → EC2 Instances
5. **Database** → RDS Cluster
6. **Storage** → S3 Buckets
7. **Monitoring** → CloudWatch

## Resource Relationships

```hcl
# VPC provides network foundation
module "vpc" {
  source = "./modules/vpc"
  # outputs: vpc_id, subnet_ids, security_group_ids
}

# EC2 uses VPC resources
module "ec2" {
  source = "./modules/ec2"
  vpc_id = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
}

# RDS uses VPC for networking
module "rds" {
  source = "./modules/rds"
  vpc_id = module.vpc.vpc_id
  db_subnet_group = module.vpc.db_subnet_group
}

# IAM provides access control
module "iam" {
  source = "./modules/iam"
  ec2_instance_role = module.ec2.instance_role
  rds_role = module.rds.access_role
}
```
