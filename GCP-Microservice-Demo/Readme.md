# 🚀 Microservices Deployment with Helm & Helmfile

[![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.28-blue?logo=kubernetes)](https://kubernetes.io/)
[![Helm](https://img.shields.io/badge/Helm-3.14+-informational?logo=helm)](https://helm.sh/)
[![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)](https://opensource.org/licenses/Apache-2.0)
![Docker](https://img.shields.io/badge/Container-Docker-blue?logo=docker)
![License](https://img.shields.io/badge/Practice-DevOps-green)
[![GitHub Stars](https://img.shields.io/github/stars/GoogleCloudPlatform/microservices-demo?style=social)](https://github.com/GoogleCloudPlatform/microservices-demo)

---

## 📖 Overview

This repository demonstrates how to deploy the [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo) application using **Helm** and **Helmfile**.

You can deploy:
- ✅ Each service one-by-one (granular control)
- ✅ Entire infrastructure in a single command with `helmfile`

---

## Architecture Diagram

![MicroService Flow](flowchart.png)
## Components Used

---

- **Deployments**  
  - **10 Microservices**   
  - **1 Redis for cart**

- **Services**  
  - **10 cluster IP** → For internal communication  
  - **1 External Service** → LoadBalancer For external consumers to access the Web UI  

- **Volume**  
  - Empty Volume for the redis to cache data for cart  
---

## 🛠️ Prerequisites

Make sure you have the following installed:

- [Helm 3+](https://helm.sh/docs/intro/install/)  
- [Helmfile](https://helmfile.readthedocs.io/en/latest/#installation)  
- [Kubernetes Cluster (Minikube / GKE / EKS / AKS)](https://kubernetes.io/docs/setup/)  
- `kubectl` CLI  

---

## ⚙️ Deploying Each Service Individually

You can deploy microservices one by one using Helm charts.

### 1️⃣ Email Service Deployment

```bash
# Create Helm chart structure
$ helm create microservice

# Substitute values and render templates for verification
$ helm template -f values/email-service-values.yaml chart/microservice

# Perform lint check
$ helm lint -f values/email-service-values.yaml chart/microservice

# Check running resources
$ kubectl get all

# Deploy email-service
$ helm install -f values/email-service-values.yaml emailservice chart/microservice

# Verify running pods
$ kubectl get all

```

### 2️⃣ Redis Service Deployment

```bash

# Create Helm chart structure
$ helm create redis

# Substitute values and render templates
$ helm template -f values/redis-values.yaml chart/redis

# Perform lint check
$ helm template -f values/redis-service-values.yaml chart/redis

# Deploy Redis service
$ helm install -f values/redis-values.yaml rediscart chart/redis

```

### 🌐 Deploying Entire Infrastructure with Helmfile

```bash 

# Sync and deploy all services
$ helmfile sync

# List deployed infrastructure
$ helmfile list

# Verify running pods
$ kubectl get all

# Destroy/uninstall infrastructure
$ helmfile destroy

```