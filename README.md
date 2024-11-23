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
**1. AWS Setup**

  1.1 Create a User with Permissions

   - Create an AWS IAM user and attach the AmazonEBSCSIDriverPolicy.

1.2 Create Access Keys

   - Generate access and secret keys for the user.

1.3 Create a Role with Permissions

   - Create an IAM role and attach the AmazonEBSCSIDriverPolicy.
     
**2. Kubernetes Setup**

2.1. Verify EBS CSI Driver

   - ensure that the EBS CSI driver is correctly installed:
     - kubectl get csidriver
     - kubectl get csinode
    
2.2. Create Secrets for AWS Credentials

   - allow Kubernetes to communicate with AWS EBS, create a secret:
     - kubectl create secret generic aws-secret \
       --namespace kube-system \
       --from-literal "key_id=<ACCESS_KEY_ID>" \
       --from-literal "access_key=<SECRET_ACCESS_KEY>"

**3. MongoDB Deployment**

3.1. Create Secrets for MongoDB

   - Generate base64-encoded values for the username and password:
      Here's the updated and organized README.md to include both AWS and Kubernetes deployment steps:
MongoDB and Mongo Express Deployment with AWS EBS

This project demonstrates the deployment of a MongoDB application on Kubernetes using AWS EBS as a persistent storage solution. It also includes Mongo Express for managing the database via a web-based interface.
Architecture Overview

The architecture comprises the following components:

    MongoDB: A NoSQL database deployed on Kubernetes, backed by AWS EBS for persistent storage.
    Mongo Express: A web-based interface for managing MongoDB, exposed via a LoadBalancer.
    Kubernetes Secrets: Securely managing sensitive data such as credentials.

Prerequisites

    Kubernetes Cluster:
        With sufficient resources for the applications.
        kubectl configured to manage the cluster.

    AWS Setup:
        AWS account with the following permissions:
            AmazonEBSCSIDriverPolicy
        AWS CLI configured with access and secret keys.

    Required Tools:
        Docker and kubectl installed on your local machine.
        Basic understanding of Kubernetes YAML files.

Steps to Deploy
1. AWS Setup
1.1. Create a User with Permissions

    Create an AWS IAM user and attach the AmazonEBSCSIDriverPolicy.

1.2. Create Access Keys

    Generate access and secret keys for the user.

1.3. Create a Role with Permissions

    Create an IAM role and attach the AmazonEBSCSIDriverPolicy.

2. Kubernetes Setup
2.1. Verify EBS CSI Driver

Run the following commands to ensure that the EBS CSI driver is correctly installed:

kubectl get csidriver
kubectl get csinode

2.2. Create Secrets for AWS Credentials

To allow Kubernetes to communicate with AWS EBS, create a secret:

kubectl create secret generic aws-secret \
    --namespace kube-system \
    --from-literal "key_id=<ACCESS_KEY_ID>" \
    --from-literal "access_key=<SECRET_ACCESS_KEY>"

3. MongoDB Deployment
3.1. Create Secrets for MongoDB

Generate base64-encoded values for the username and password:

echo -n 'your-username' | base64
echo -n 'your-password' | base64
     



## 5. Cleanup

 **To delete all resources:**

- kubectl delete -f mongodb-project/

