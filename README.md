![2](https://github.com/user-attachments/assets/34a7c34c-0f55-4b36-ac24-bf404febc77d)

# MongoDB and Mongo Express Deployment with AWS EBS

This project demonstrates the deployment of a MongoDB application on Kubernetes using AWS EBS as a persistent storage solution. It also includes Mongo Express for managing the database via a web-based interface.
Architecture Overview

## The architecture comprises the following components:

   - MongoDB: A NoSQL database deployed on Kubernetes, backed by AWS EBS for persistent storage.
   - Mongo Express: A web-based interface for managing MongoDB, exposed via a LoadBalancer.
   - Kubernetes Secrets: Securely managing sensitive data such as credentials.

# Prerequisites

   - Kubernetes Cluster with sufficient resources.
   - AWS account with the following permissions:
   -     AmazonEBSCSIDriverPolicy
   - AWS CLI and kubectl configured to manage resources.

# Steps to Deploy
  1. AWS Setup
  1.1 Create a User with Permissions

   - Create an AWS IAM user and attach the AmazonEBSCSIDriverPolicy.

1.2 Create Access Keys

   - Generate access and secret keys for the user.

1.3 Create a Role with Permissions

   - Create an IAM role and attach the AmazonEBSCSIDriverPolicy.

## 5. Cleanup

 **To delete all resources:**

- kubectl delete -f mongodb-project/

