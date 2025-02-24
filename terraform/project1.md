# Project 1: Cisco DevOps 300‑910: Automating Infrastructure

## Overview
This project focuses on automating infrastructure using Terraform as part of the Cisco DevOps 300‑910 course.

## Objectives
- Automate the deployment of infrastructure components.
- Implement best practices for infrastructure as code.

## Steps
1. **Step 1**: Initialize the Terraform configuration.
2. **Step 2**: Define the infrastructure resources.
3. **Step 3**: Apply the configuration to provision the resources.

## Code Snippets
```hcl
# Example Terraform configuration
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  