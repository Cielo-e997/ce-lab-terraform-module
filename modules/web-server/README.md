# Web Server Module

This module creates:

- A VPC
- Public subnets
- Internet Gateway
- Route tables

## Inputs

- project_name
- environment
- vpc_cidr
- availability_zones
- public_subnet_cidrs
- private_subnet_cidrs

## Outputs

- vpc_id
- public_subnet_ids
