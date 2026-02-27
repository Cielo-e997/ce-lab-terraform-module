# Lab M4.05 – Reusable Terraform Module

This lab demonstrates how to:

- Create a reusable Terraform module
- Define inputs and outputs
- Use the module in a root configuration
- Organize a clean repository structure

## Repository Structure

ce-lab-terraform-module/
├── README.md
├── main.tf (uses module)
├── modules/
│   └── web-server/
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
│       └── README.md
└── screenshots/

## Usage

The root configuration calls the web-server module located in:

./modules/web-server

Run:

terraform init
terraform plan
terraform apply
