# java-eks-project
This repository deploys basic java application in AWS EKS infrastructure provisioned using Terraform using Github Actions.

## Prerequisites

- AWS account with read and write permissions to create EKS, VPC, ECR, S3, EC2 and IAM resources
- Generate access key and secret key for that account to be used for configuring aws credentials
- For this project we will be using aws region eu-north-1

## Usage

### Configure AWS credentials as GH secrets
Add AWS access key and secret key for the user to the GitHub secrets as repository secrets.
Go to repository settings > Secrets and variables > Actions > New Repository Secret.
Add the values.

### Github Actions workflow Steps
- Checkout code (SCM)
- Set short git commit SHA -> to get the short version of the commit sha for the image
- Set up JDK 22 -> For java applications JDK is required
- Build with Maven -> Our application uses maven hence maven commands to build and test
- Configure AWS credentials -> This uses GH Secrets to set the credentials in the GH Actions server to connect to the correct AWS account
- Login to Amazon ECR -> connect to the ECR in the same region in AWS for image management
- Build, tag, and push image to Amazon ECR
- - build, tag and pushing image to the AWS ECR using variables and shortened commit SHA to generate new image on every build
- Setup kubectl
- - k8s CLI (kubectl) is required for the deployment of the applications using their yaml files
- Update kubeconfig
- - Configuring kubeconfig to connect to the terraform provisioned AWS EKS cluster and to deploy app in the same
- Deploy to EKS
- - Deploys the application by applying the deployment and service using their yamls by replacing image with the latest one everytime their is a new build and image available

