**MERN TODO App — End-to-End DevOps Project**
Overview

This repository showcases a complete CI/CD pipeline implementation for a MERN stack application.
What started as a raw MERN Todo App evolved into a production-ready deployment running on a self-hosted Kubernetes cluster, fully automated with Jenkins + ArgoCD.

Everything was built from scratch on bare-metal/on-premise infra, simulating a real-world enterprise environment.


**Project Evolution**

**Development Phase**

Built a raw MERN TODO app (frontend + backend).
Connected to MongoDB.
Verified app in dev mode.


**Dockerization**
Backend → Dockerized with Node.js, connected to MongoDB.
Frontend → Dockerized React app with NGINX reverse proxy.
Created a custom Docker network for service communication.
Used Docker Compose for multi-service orchestration.
Persistent storage via volumes for MongoDB.


**Kubernetes Migration**
Set up a kubeadm cluster (1 master + 1 worker).
Deployed frontend, backend, MongoDB with manifests.
Migrated MongoDB into a StatefulSet with:
Headless Service
PersistentVolume (PV) & PersistentVolumeClaim (PVC)
Ensured data persistence across pod restarts.


**Observability & Load Testing**
Load-tested with Apache Benchmark (ab).
Integrated Prometheus + Grafana (via Helm).
Observed CPU/memory spikes with increasing users.


**Networking & Load Balancing**
Deployed MetalLB for LoadBalancer IP assignment.
Configured NGINX Ingress Controller for routing.
External access enabled via LAN subnet dynamic IPs.


**Security Enhancements**
Exposed application via HTTPS using Cloudflared Tunnel with a free domain.
Kubernetes Secrets & ConfigMaps for sensitive data.
Migrated secrets management to HashiCorp Vault.


**GitOps with ArgoCD**
Installed ArgoCD and connected to this repo.
Configured Helm charts for manifests.
Enabled auto-sync → cluster always matches GitHub state.


**CI/CD with Jenkins**
Jenkins pipeline stages:

1st stage---> Checkout Code or code clone 

2nd stage---> Build Docker Images (frontend + backend)

3rd stage---> Push Images to Docker Hub

4th stage---> Update K8s Manifests with new image tags

5ht stage---> Commit & Push Changes back to GitHub (triggers ArgoCD sync)
