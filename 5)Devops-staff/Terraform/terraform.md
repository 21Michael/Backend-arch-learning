# Terraform

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform 
can manage existing and popular service providers as well as custom in-house solutions.

**The key features of Terraform are:**
  - **Infrastructure as Code:**  
    Infrastructure is described using a high-level configuration syntax. This allows a blueprint of your
    datacenter to be versioned and treated as you would any other code. Additionally, infrastructure can
    be shared and re-used.
  - **Execution Plans:**  
    Terraform has a "planning" step where it generates an execution plan. The execution plan shows what 
    Terraform will do when you call apply. This lets you avoid any surprises when Terraform manipulates
    infrastructure.
  - **Resource Graph:**  
    Terraform builds a graph of all your resources, and parallelizes the creation and modification of 
    any non-dependent resources. Because of this, Terraform builds infrastructure as efficiently as possible,
    and operators get insight into dependencies in their infrastructure.
  - **Change Automation:**  
    Complex changesets can be applied to your infrastructure with minimal human interaction. With the 
    previously mentioned execution plan and resource graph, you know exactly what Terraform will change 
    and in what order, avoiding many possible human errors.

## Declare File Syntax:
### 1) Providers:
Terraform relies on plugins called providers to interact with cloud providers, SaaS providers, and other APIs.
Terraform configurations must declare which providers they require so that Terraform can install and use them.  
https://registry.terraform.io/browse/providers
1) Declare the providers used in project (not required):
    ```text
      // AWS Example:
      terraform {
        required_providers {
          aws = {
            source = "hashicorp/aws"
            version = "4.32.0"
          }
        }
      }
    ```

2) Add the provider to the infrastructure config file:
    ```text
      // AWS Example:
      provider "aws" {
        version = ""
        region = ""
        access_key = ""
        secret_key = ""
      }
    ```
3) Install the providers:
   Command:
    ```text
      terraform init
    ```

### 2) Resources:
Resources are the most important element in the Terraform language. Each resource block describes one or 
more infrastructure objects, such as virtual networks, compute instances, or higher-level components such 
as DNS records.   
```text
  resource "resource_name" "variable_name" {
    input_attribute_name = "value"
  }
  
  // AWS VPC Example:
  resource "aws_vpc" "myapp-vpc" {
    cidr_block = "10.0.0.0/16"
    tags = {
        Name: 'client-vpc'
    }
  }
```
  - **Attributes:**  
    Every resource has its own attributes for set up (`Inputs`) and after set up (`Outputs`) that can be 
    reached from other resources;
    ```text
        resource "resource_name" "variable_name" {
          input_attribute_name = "value" // !!!!!!!!!!!!!!!!!
        }
    
        resource "resource_name" "variable_name" {
          input_attribute_name = resource_name.variable_name.output_attribute_name // !!!!!!!!!!!!!!!!
        }
    ```
  - **Meta-Attributes:**  
    https://www.terraform.io/language/resources/syntax#meta-arguments  
    The Terraform language defines several meta-arguments, which can be used with any resource type to
    change the behavior of resources.
     - **depends_on:** for specifying hidden dependencies
     - **count:** for creating multiple resource instances according to a count
     - **for_each:** to create multiple instances according to a map, or set of strings
     - **provider:** for selecting a non-default provider configuration
     - **lifecycle:** for lifecycle customizations
     - **provisioner:** for taking extra actions after resource creation

### 3) Data Sources:
Data sources allow Terraform to use information defined outside of Terraform, defined by another separate 
Terraform configuration, or modified by functions. By it, we can reach the already existing resources;
```text
 data "resource_name" "variable_name" {
    input_attribute_name = "value"
  }
```
  - **Attributes:**  
    Every resource has own `Data Sources` attributes:  
    AWS Example: https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/vpc
    ```text
      data "aws_vpc" "default" {
        default = true // Select the existing default VPC; !!!!!!!!!!!!!!!!!!!
      }
    
      resource "aws_subnet" "example" {
        vpc_id            = data.aws_vpc.default.id // Use default VPC !!!!!!!!!!!!!!!!!!!
        availability_zone = "us-west-2a"
        cidr_block        = cidrsubnet(data.aws_vpc.selected.cidr_block, 4, 1)
      }
    ```
    
### 4) State:
Terraform must store state about your managed infrastructure and configuration. This state is used by 
Terraform to map real world resources to your configuration, keep track of metadata, and to improve 
performance for large infrastructures.

This state is stored by default in a local file named `"terraform.tfstate"`, but it can also be stored remotely,
which works better in a team environment.

  - **State Storage:**
    - **local**
    - **cloud**
  
  - **State Commands:**
    - `terraform state pull`  
      This will load your remote state and output it to stdout.
    - `terraform state push`  
      This will overwrite the remote state. This can be used to do manual fixups if necessary.
    

### 5) Variables (Input / Output)

### **<ins>Input:</ins>**
Input variables let you customize aspects of Terraform modules without altering the module's own source code.
This functionality allows you to share modules across different Terraform configurations, making your module 
composable and reusable.  
  - **Declare:**  
    ```text
      variable "image_id" {
        type = string
      }
      
      variable "availability_zone_names" {
        type    = list(string)
        default = ["us-west-1a"]
      }
      
      variable "docker_ports" {
        type = list(object({
          internal = number
          external = number
          protocol = string
        }))
        default = [
          {
            internal = 8300
            external = 8300
            protocol = "tcp"
          }
        ]
      }
    ```
    
  - **Assigning variables:**
    - in console when running `terraform apply`
    - in console when running `terraform apply -var "var_name=value"`
    - inside variable file `terraform.tfvars`
      ```text
        var_name = value
      ```

  - **Usage:**  
    ```text
      resource "resource_name" "variable_name" {
        input_attribute_name = var.var_name // variable usage
      }
    ```

  - **Arguments:**  
    - **default** - A default value which then makes the variable optional.
    - **type** - This argument specifies what value types are accepted for the variable.
    - **description** - This specifies the input variable's documentation.
    - **validation** - A block to define validation rules, usually in addition to type constraints.
    - **sensitive** - Limits Terraform UI output when the variable is used in configuration.
    - **nullable** - Specify if the variable can be null within the module.

### **<ins>Output:</ins>**
Output values make information about your infrastructure available on the command line, and can expose 
information for other Terraform configurations to use. Output values are similar to return values in
programming languages.
```text
  output "instance_ip_addr" {
    value = aws_instance.server.private_ip
  }
```
  - **Custom Condition Checks:**  
    You can use precondition blocks to specify guarantees about output data. The following examples creates 
    a precondition that checks whether the EC2 instance has an encrypted root volume.
    ```text
      output "api_base_url" {
        value = "https://${aws_instance.example.private_dns}:8433/"
      
        # The EC2 instance must have an encrypted root volume.
        precondition {
          condition     = data.aws_ebs_volume.example.encrypted
          error_message = "The server's root volume is not encrypted."
        }
      }
    ```
    
### 6) Env variables
Terraform refers to a number of environment variables to customize various aspects of its behavior. None of 
these environment variables are required when using Terraform, but they can be used to change some of 
Terraform's default behaviors in unusual situations, or to increase output verbosity for debugging.  
https://www.terraform.io/cli/config/environment-variables

  - **TF_LOG**  
    Enables detailed logs to appear on stderr which is useful for debugging.
    ```text
      export TF_LOG=trace
    ```
  - **TF_LOG_PATH**  
    This specifies where the log should persist its output to. Note that even when TF_LOG_PATH is set, 
    TF_LOG must be set in order for any logging to be enabled.
    ```text
      export TF_LOG_PATH=./terraform.log
    ```
  - **TF_VAR_name**  
    Environment variables can be used to set variables. The environment variables must be in the format
    TF_VAR_var_name and this will be checked last for a value. For example `.env` file:
    ```text
      TF_VAR_region=us-west-1
      TF_VAR_ami=ami-049d8641
      TF_VAR_alist='[1,2,3]'
      TF_VAR_amap='{ foo = "bar", baz = "qux" }'
    ```
  - ...

### 7) Modules
Modules are containers for multiple resources that are used together. A module consists of a collection of .tf
and/or .tf.json files kept together in a directory.

### Structure:
  - **The Root Modules:**    
    - `main.tf` (define providers and child modules)  
      Root `main.tf` file structure:
      ```text
        module "module_name" {
          source  = "path to the module"
          version = "0.0.5"
          
          input_variable_name = value
        }
      ```
    - `variables.tf` (passed to the child modules variables)  
    - `outputs.tf` (main outputs)  
      - **Child Modules:**
        - `main.tf` (recourses, data)
        - `variables.tf` (variables of the current module and passed from the root module)  
        - `outputs.tf` (outputs of the current module, it will allow reaching resources of the module inside 
          the main module)  


## Commands:
https://www.terraform.io/cli/commands

  - ### init          
    Prepare your working directory for other commands;
  - ### validate      
    Check whether the configuration is valid;
  - ### plan          
    Show changes required by the current configuration;
  - ### apply         
    Create or update infrastructure;
  - ###destroy       
    Destroy previously-created infrastructure;
