# IAS

Links->

https://www.terraform.io/

https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started

https://github.com/hashicorp/terraform-provider-aws/tree/master/examples

Steps for IAS using Aws
-----------------------
Prerequisites
To follow this tutorial you will need:

The Terraform CLI (0.14.9+) installed.  -> https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started
The AWS CLI installed.-> https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
An AWS account. -> 

Your AWS credentials. You can create a new Access Key on this page.

1)https://console.aws.amazon.com/iam/home?#/security_credentials
Configure the AWS CLI from your terminal. Follow the prompts to input your AWS Access Key ID and Secret Access Key.

--> aws configure
You need to provide your Access Key ID & Secret Access Key

Access Key ID:
AKIAXE67W4SUSBL645EI
Secret Access Key:
nPpDPKnsKXMOLC7uj9V0FPDA+MEjJrmbPOrKO03W


2)Each Terraform configuration must be in its own working directory. Create a directory for your configuration.
mkdir learn-terraform-aws-instance

3)Change into the directory.
cd learn-terraform-aws-instance

4)Create a file to define your infrastructure i.e main.tf  

  You will write your first configuration to define a single AWS EC2 instance
  
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.27"
    }
  }

  required_version = ">= 0.14.9"
}

provider "aws" {
  profile = "default"
  region  = "us-west-2"
}

resource "aws_instance" "app_server" {
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"

  tags = {
    Name = "MotorAppServerInstance"
  }
}

5)inciatization of tarraform
->terraform init

6)Format and validate the configuration
->terraform fmt
->terraform validate


7)Plan the infrastucture
->terraform plan 

8)Create infrastructure
->terraform apply

9)Inspect state
->terraform show

10)Manually Managing State
 you may want a list of the resources in your project's state, which you can get by using the list subcommand
 ->terraform state list
 
11) Change Configuration
  resource "aws_instance" "app_server" {
-  ami           = "ami-830c94e3"
+  ami           = "ami-08d70e59c07c61a3a"
 instance_type = "t2.micro"
}

This update changes the AMI to an Ubuntu 16.04 AMI. The AWS provider knows that it cannot change the AMI of an instance after it has been created, so Terraform will destroy the old instance and create a new one.

12)Apply Changes -> terraform apply
 
13)Destory Changes -> terraform destroy
