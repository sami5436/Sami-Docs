# Terraform 

During my time at ExxonMobil, I had the privilege of working with a powerful and emerging tool called **Terraform**. Terraform is an Infrastructure as Code (IaC) tool that enables cloud engineers to build, deploy, and manage cloud infrastructure using a simple, declarative language. It allows for scalable, version-controlled infrastructure deployments across cloud providers like AWS, Azure, and GCP.

#### Benefits of Terraform  

- **Infrastructure as Code (IaC):**  
  Terraform allows you to define and provision infrastructure using configuration files, enabling version control and automation.

- **Cloud-Agnostic:**  
  Terraform works with multiple cloud providers (AWS, Azure, GCP) and other platforms through a wide range of providers.

- **Declarative Configuration:**  
  You describe your desired infrastructure state, and Terraform determines the necessary steps to reach that state.

- **Execution Planning:**  
  The `terraform plan` command provides a preview of the changes Terraform will make before applying them, allowing for safer deployments.

- **Change Automation:**  
  Automatically applies incremental changes to infrastructure, minimizing the risk of manual errors.

- **State Management:**  
  Maintains a state file that maps your configuration to real-world infrastructure, ensuring accurate updates.

- **Modular Design:**  
  Enables code reuse and abstraction through modules, making infrastructure code more maintainable and scalable.

- **Collaboration Support:**  
  Teams can collaborate effectively by sharing infrastructure code through version control and using backends for remote state storage and locking.

- **Integration with CI/CD Pipelines:**  
  Easily integrates into DevOps workflows, enabling automated testing and deployment of infrastructure.

- **Policy and Governance (via TFE/TFC):**  
  Organizations can enforce security and compliance policies, manage users and permissions, and audit changes using Terraform Enterprise or Terraform Cloud.

**Core Components of Terraform:**
- **Providers**:
  - Plugins that interact with APIs of cloud platforms and services (AWS, Azure, GitHub). They define what infrastructure Terraform can manage.
  - ```hcl
    provider "aws" {
      region = "us-east-1"
    }
    ```
  - This tells Terraform to use the AWS provider and deploy resources in the us-east-1 region.
- **Resources**:
  - The basic building blocks in Terraform. Each resource corresponds to an infrastructure object (like an EC2 instance, a storage account, etc).
  - ```hcl
    resource "aws_s3_bucket" "my_bucket" {
      bucket = "my-unique-bucket-name"
      acl    = "private"
    }
    ```
  -  This defines an S3 bucket resource named my_bucket.

- **Modules**:
  - Self-contained packages of Terraform configurations. They help reuse code and organize complex infrastructure
  - ```hcl
    module "vpc" {
      source  = "./modules/vpc"
      cidr_block = "10.0.0.0/16"
    }
    ```
  - This calls a local VPC module and passes in a variable.
- **Variables**:
  - Inputs that allow configurations to be dynamic and reusable. Can be defined using variable blocks and passed via CLI, environment, or .tfvars files.
  - ```hcl
    variable "instance_type" {
      description = "EC2 instance type"
      type        = string
      default     = "t2.micro"
    }
    ```
  - You can override this value via CLI or `.tfvars` file.
- **Outputs**:
  - Values you want to extract from your Terraform configuration, useful for debugging or passing data between modules.
  - ```hcl
    output "bucket_name" {
      description = "Name of the S3 bucket"
      value       = aws_s3_bucket.my_bucket.bucket
    }
    ```
  - Used to display values after `terraform apply`.
- **State**:
  - Terraform uses a state file (terraform.tfstate) to map real-world infrastructure to your config. This file is critical for tracking changes and performing updates efficiently
  - Sometimes this is stored in storage on cloud if Terraform open source is used. This is done to ensure everyone is using the same version of the state file.
  - ```hcl
    terraform {
      backend "s3" {
        bucket         = "my-terraform-state-bucket"
        key            = "prod/terraform.tfstate"
        region         = "us-east-1"
        dynamodb_table = "terraform-locks"
        encrypt        = true
      }
    }
    ```
  - This example stores your state in an S3 bucket with state locking via DynamoDB.

- **Backend**:
  - Defines how and where Terraform stores its state. Common backends include local, S3 with DynamoDB locking, Azure Storage Account, or remote via Terraform Cloud. (Mentioned in state section).
- Lifecycle Rules:
  - Allow for finer control of resource behavior, such as create_before_destroy, ignore_changes, etc.
  - ```hcl
    resource "aws_instance" "web" {
      ami           = "ami-0c55b159cbfafe1f0"
      instance_type = var.instance_type
    
      lifecycle {
        create_before_destroy = true
        ignore_changes        = [tags]
      }
    }
    ```
  - Helps control how Terraform handles updates to resources.
- **Data Sources**:
  - Used to fetch information from providers (e.g., get the latest AMI ID from AWS) without creating new resources.
  - ```hcl
    data "aws_ami" "latest_amazon_linux" {
      most_recent = true
      owners      = ["amazon"]
    
      filter {
        name   = "name"
        values = ["amzn2-ami-hvm-*-x86_64-gp2"]
      }
    }
    ```
  - This fetches the latest Amazon Linux 2 AMI ID.





