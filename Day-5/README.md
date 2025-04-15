# Day 5 - Introduction to Kubernetes

## Overview

Day 5 introduced Kubernetes as a powerful container orchestration tool that solves limitations of containers like lack of auto-scaling, load balancing, and self-healing. You learned about Kubernetes architecture, components (master and worker nodes), manifest files, and set up a Kubernetes cluster using EKS on AWS. The session also covered creating pods, understanding key YAML fields, and running basic Kubernetes commands.

---

## Problems with Containers

- **Containers will not support Auto Scaling**  
  - **Scale up**: Whenever traffic increases, we need to manually increase the number of servers.
  - **Vertical Scaling**: Increases system resources (e.g., CPU, RAM) on the same server.
  - **Horizontal Scaling**: Adds more servers to the existing infrastructure to handle increased traffic.
  - **Scale down**: When traffic goes down, we must remove the additional servers to save resources.

- **Containers do not support Load Balancing**  
  Containers cannot automatically distribute traffic across multiple containers.

- **Containers do not support Self-Healing**  
  If a container goes down, it results in application downtime, as containers cannot recover on their own.

---

## Solution: Kubernetes Orchestration

To solve these issues, we turn to **Kubernetes**, a container management tool. Kubernetes automates and manages containers by providing several key features:

- **Orchestration**: Automates the deployment and management of containers.
- **Auto-scaling**: Automatically adjusts the number of containers based on demand.
- **Load Balancing**: Distributes traffic evenly across containers.
- **Self-Healing**: Restarts or replaces failed containers automatically.

Kubernetes is **platform-independent** and can run on any cloud provider or on-premises infrastructure.

---

## Kubernetes Manifest Files

To perform automation with Kubernetes, we use **Kubernetes manifest files** (written in YAML), which define the desired state of the application.

---

## Setup Kubernetes

1. **Create and Install Cluster Setup Script**

   - Open the terminal and create a script file:  
     `vi cluster.sh`

   - Copy and paste the content from [this link](https://github.com/Msocial123/EverNorth-DevOps-Training-Material/blob/main/Install%20EKSCTL%2CKubectl%2CAWS%20CLI.sh).

   - Save and close:  
     `esc -> :wq`

   - Make the script executable:  
     `sudo su`  
     `chmod 777 cluster.sh`

   - Run the script to install all required packages:  
     `sh cluster.sh`

2. **Create IAM User for EKS**

   - Go to **IAM → Users → Create User**.  
     - Give the user a name.
     - Do **not** check any checkboxes.
     - Click **Create**, then go to **Next** and attach the **AdministratorAccess** policy.
     - Create and download the CSV file (it contains your access and secret keys).

3. **Configure AWS CLI**

   Run the following command to configure the AWS CLI:  
   `aws configure`

   Enter the required details:
   - **AWS Access Key**
   - **Secret Access Key**
   - **Region**
   - **Output Format**

4. **Create the Kubernetes Cluster**

   Use **eksctl** to create a Kubernetes cluster:  

   ```bash
   eksctl create cluster --name ranjana-cluster --version 1.31 --region ap-south-1 --nodegroup-name test-linux --node-type t2.micro --nodes 3 --nodes-min 3 --nodes-max 5 --managed

---

## Kubernetes Cluster and Nodes

A Kubernetes Cluster is a group of nodes. It consists of two types of nodes:

## Master Node

- The hero of the cluster, responsible for the overall health and management of the cluster. It ensures that the desired state matches the actual state.

## Worker Node

- Where your applications are deployed. At least one worker node is needed to run applications in the cluster.

---

## Types of Clusters

## On-Premise Cluster

- Managed by you. You are responsible for everything, including handling any application downtime.

## Cloud-Managed Cluster

- Managed by the cloud provider. In AWS, this is done using Elastic Kubernetes Service (EKS), where AWS manages the master node and you focus on the worker nodes.

---

## Master Node Components

## API Server

- The frontend for the Kubernetes control plane. It handles requests for scaling, load balancing, and other operations.

## ETCD

- A distributed database that stores all cluster data, including application configurations.

## Controllers

- Monitor the health of applications and ensure the desired state matches the actual state.

## Scheduler

- Responsible for scheduling pods onto worker nodes. Pods are the smallest deployable units in Kubernetes.

---

## Worker Node Components

## Kubelet

- Responsible for managing pods. It ensures that containers in pods are running and healthy.

## Container Runtime

- Manages container lifecycles. It pulls Docker images, creates containers, and starts them.

## Kube-Proxy

- A networking component that ensures communication between pods and external services.

---

## Pods

- Pods are the smallest deployable units in Kubernetes. A pod can contain one or more containers that share storage and networking.

---

## Kubernetes Manifest File Structure

A Kubernetes manifest file is written in YAML format. It defines the desired state of Kubernetes objects, such as Pods or Deployments.

## Key Fields in a Manifest

- **apiVersion**: Defines the version of the Kubernetes API.
  
- **kind**: Specifies the type of object (e.g., Pod, Deployment).
- **metadata**: Assigns labels and other metadata to the object.
- **spec**: Defines the desired state and behavior of the object.

---

## Useful Kubernetes Commands

## Deploy the Pod

```bash
kubectl apply -f pod.yaml
```

## List Running Pods

```bash
kubectl get pods
```

## Show More Info about Pods

```bash
kubectl get pods -o wide
```

```bash
kubectl describe pod sample-pod
```

## Kubernetes Resource Units

- **1 CPU** = 1000 millicores (m)
- **1 GB RAM** = 1024 Mebibytes (Mi)
