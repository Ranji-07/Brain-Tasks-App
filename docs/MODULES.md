# 📋 Terraform Modules Documentation

## VPC Module

### Purpose
Creates networking infrastructure including VPC, subnets, and routing.

### Variables
```hcl
vpc_cidr              = "10.0.0.0/16"
availability_zones    = ["us-east-1a", "us-east-1b"]
enable_nat_gateway    = true
enable_dns_hostnames  = true
```

### Outputs
```hcl
vpc_id
vpc_cidr_block
public_subnet_ids
private_subnet_ids
security_group_ids
```

## EC2 Module

### Purpose
Manages compute instances, security groups, and auto-scaling.

### Variables
```hcl
instance_type    = "t3.medium"
instance_count   = 2
ami_id          = "ami-0c02fb55ab2a9b6b2"
key_name        = "my-key"
```

### Outputs
```hcl
instance_ids
private_ips
public_ips
security_group_id
```

## RDS Module

### Purpose
Provisions managed database services.

### Variables
```hcl
engine              = "postgres"
engine_version      = "15.0"
instance_class      = "db.t3.micro"
allocated_storage   = 20
db_name            = "appdb"
username           = "admin"
```

### Outputs
```hcl
db_instance_endpoint
db_name
db_port
```

## S3 Module

### Purpose
Manages object storage buckets.

### Variables
```hcl
bucket_name                = "my-app-bucket"
versioning_enabled         = true
server_side_encryption     = true
public_access_block        = true
```

## IAM Module

### Purpose
Manages identity and access control.

### Variables
```hcl
role_name              = "app-role"
policy_documents       = []
role_description       = "Application role"
```

For complete documentation, see each module's README.
