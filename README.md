# AWS-Terraform
Linking AWS IAM Token and Terraform for S3 Bucket Creation and Upload
In this project, I successfully linked an AWS Identity and Access Management (IAM) token and a Terraform token to automate the process of creating a new Amazon S3 bucket and uploading files to it. Below are the steps I followed to accomplish this:

Step 1: Setting Up IAM Permissions
Create an IAM User:

I started by creating a new IAM user in the AWS Management Console with programmatic access. This user would be responsible for managing the S3 bucket.
Attach Policies:

Next, I attached the necessary permissions to the IAM user by adding a policy that allowed actions such as s3:CreateBucket, s3:PutObject, and s3:GetObject. This ensured the user had the required access to manage S3 resources.
Retrieve IAM Credentials:

After setting up the IAM user, I obtained the AWS Access Key ID and Secret Access Key. These credentials are critical for authenticating with AWS services programmatically.
Step 2: Configuring Terraform
Install Terraform:

I ensured that Terraform was installed on my local machine. This tool allows for infrastructure as code (IaC) and simplifies the management of cloud resources.
Create Terraform Configuration:

I created a new Terraform configuration file (e.g., main.tf) where I defined the desired state of my infrastructure. In this file, I specified the provider as AWS and configured it with the IAM credentials I retrieved earlier:

hcl
provider "aws" {
  region     = "us-west-2"
  access_key = "<YOUR_AWS_ACCESS_KEY>"
  secret_key = "<YOUR_AWS_SECRET_KEY>"
}
Define the S3 Bucket:

I then defined a new S3 bucket resource in the configuration file:

hcl
resource "aws_s3_bucket" "my_personal_bucket" {
  bucket = "my-unique-bucket-name"
  acl    = "private"
}
Step 3: Deploying with Terraform
Initialize Terraform:

I ran the terraform init command to initialize the Terraform configuration and download the required provider plugins.
Plan the Infrastructure:

I executed terraform plan to review the changes that Terraform would make to achieve the desired state. This step helped confirm that my configurations were correct.
Apply the Changes:

After confirming the plan, I ran terraform apply, which prompted me for confirmation. Upon acceptance, Terraform created the S3 bucket in AWS as specified.
Step 4: Uploading Files to the S3 Bucket
Using AWS CLI for File Upload:

To upload files to the newly created S3 bucket, I utilized the AWS CLI. I configured the CLI with the same IAM credentials used in Terraform by running:

bash
aws configure
I provided the Access Key ID, Secret Access Key, and the desired region.

Upload Files:

Finally, I uploaded files to the S3 bucket using the following command:

bash
aws s3 cp <local-file-path> s3://my-unique-bucket-name/
This streamlined process effectively demonstrates how to leverage AWS IAM and Terraform together to automate cloud resource management, enhancing both efficiency and reliability.

