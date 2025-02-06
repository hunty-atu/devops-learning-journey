# Terraform

## Overview
This folder contains my notes and projects related to Terraform.

## Projects
- [Project 1: Cisco DevOps 300‑910: Automating Infrastructure](project1.md)
- [Project 2: How Terraform Works: A Visual Intro](project2.md)
- [Project 3: Docker remote host - variables & outputs](project3.md)

## Learnings
- Providers wriiten in Go is plugin is a plugin that can be inserted into the Terraform configuration to add different communications functionality
- be used to create and manage a number of different types of infrastructure elements, including options like VMs, compute instances, or containers that are all referred to as resources.
- there is also a data source block. While the resource block is used to create or modify infrastructure elements, the data source block is used to query for information from a remote source or to compute data that will be used later in the configuration, for example inside a later resource block. Similar to the resource block, a data source block is configured with the name of the data source that is specified by the provider configured and an argument name where any resulting information will be exported into. Just like a resource, the specific data sources that are available depends on the specific provider being used. Another way to think of a Terraform data source is that it is essentially a read‑only version of a resource. While the data source is only available to query for information from an existing infrastructure, a resource is able to use this collected information and create new or modify existing elements.
- The input variable is used as a parameter for use inside the main Terraform configuration.The value for these variables can then be set inside the tfvars file. In this way, the person performing the configuration doesn't have to change that part of the configuration. Terraform also provides the ability to pass variable values into the configuration from the CLI.
organize your content into folders and document your learnings and projects in markdown files within your GitHub repository.
- A provisioner is used to execute external scripts after the provisioning of an infrastructure element by Terraform. These scripts are commonly used for configuration management, bootstrapping, and/or clean up. For the purposes of this course, we will use it as a way to run a separate configuration management tool to configure the elements once they are created. Terraform supports three different generic provisioners. These include a file provisioner to copy files and directories, a local‑exec provisioner to run a local script, and a remote‑exec provisions that runs a script on the created remote element.

