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
         AmazonEBSCSIDriverPolicy
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
  - create the secret YAML file 101-Secrets for MongoDB Credentials.yml:

  - Apply the secret:
    - kubectl apply -f 101-Secrets\ for\ MongoDB\ Credentials.yml
   
3.2. Create a StorageClass for MongoDB

   - Define a StorageClass for dynamic volume provisioning:

   - Apply the StorageClass:
     - kubectl apply -f 103-StorageClass.yml
    
3.3. Create a PersistentVolumeClaim

   - Create the PVC YAML:

   - Apply the PVC:
     - kubectl apply -f 104-PersistentVolumeClaim.yml
    
3.4. Deploy MongoDB

   - Create a deployment YAML file for MongoDB:
     - kubectl apply -f 105-Deploy\ MongoDB.yml
    
3.5. Expose MongoDB Service

   - Expose MongoDB as a ClusterIP service:
     - kubectl apply -f 106-Expose\ MongoDB\ Service.yml

**4. Mongo Express Deployment**

4.1. Create ConfigMap
   
   - Apply the ConfigMap:
     - kubectl apply -f 107-ConfigMap.yml

4.2. Deploy Mongo Express

   - Create a deployment YAML file for Mongo Express:
     - kubectl apply -f 108-Deploy\ Mongo\ Express.yml
    
4.3. Expose Mongo Express Service

   - Expose Mongo Express as a LoadBalancer:
     - kubectl apply -f 109-Expose\ Mongo\ Express\ Service.yml
    
**5. Verify Deployment**

   - Check the status of pods:
     - kubectl get po

   - Verify the services:
     - kubectl get svc

**5. Cleanup**

   - To delete all resources:
     - kubectl delete -f mongodb-project/

