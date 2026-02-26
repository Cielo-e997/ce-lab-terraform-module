# VPC Terraform Module

This module creates a reusable multi-AZ VPC with public and private subnets, an Internet Gateway, and optional NAT Gateway configuration.

The goal is to avoid duplicating VPC code across environments (dev, staging, prod) by using variables to control behavior.

---

## What this module creates

- A VPC with DNS support enabled
- Public subnets across multiple Availability Zones
- Private subnets across multiple Availability Zones
- Internet Gateway for public internet access
- Optional NAT Gateway (single or multi-AZ)
- Route tables and associations
- Consistent tagging across all resources

---

## Example Usage

```hcl
module "vpc" {
  source = "./modules/vpc"

  project_name         = "myproject"
  environment          = "dev"
  vpc_cidr             = "10.0.0.0/16"
  availability_zones   = ["us-east-1a", "us-east-1b"]
  public_subnet_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnet_cidrs = ["10.0.11.0/24", "10.0.12.0/24"]

  enable_nat_gateway   = true
  single_nat_gateway   = true  # Cost optimization for dev

  tags = {
    Owner = "DevTeam"
  }
}
```

---

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| project_name | Project name used for naming resources | `string` | n/a | yes |
| environment | Environment name (dev, staging, prod) | `string` | n/a | yes |
| vpc_cidr | CIDR block for the VPC | `string` | `"10.0.0.0/16"` | no |
| availability_zones | List of availability zones | `list(string)` | n/a | yes |
| public_subnet_cidrs | CIDR blocks for public subnets | `list(string)` | n/a | yes |
| private_subnet_cidrs | CIDR blocks for private subnets | `list(string)` | n/a | yes |
| enable_nat_gateway | Whether to create a NAT Gateway | `bool` | `true` | no |
| single_nat_gateway | Use a single NAT instead of one per AZ | `bool` | `false` | no |
| tags | Additional tags applied to all resources | `map(string)` | `{}` | no |

---

## Outputs

| Name | Description |
|------|-------------|
| vpc_id | ID of the created VPC |
| public_subnet_ids | IDs of the public subnets |
| private_subnet_ids | IDs of the private subnets |
| internet_gateway_id | Internet Gateway ID |
| nat_gateway_ids | NAT Gateway IDs |
| public_route_table_id | Public route table ID |
| private_route_table_ids | Private route table IDs |

---

## Notes

- For dev environments, using `single_nat_gateway = true` helps reduce costs.
- For production, consider using multiple NAT Gateways for high availability.
