# MERN TODO App — End-to-End DevOps Project

## 🚀 Overview
This repository showcases a **complete CI/CD pipeline implementation** for a MERN stack application.  
What started as a raw MERN Todo App evolved into a **production-ready deployment** running on a **self-hosted Kubernetes cluster**, fully automated with **Jenkins + ArgoCD**.  

💥 **No cloud shortcuts** — everything was built from scratch on **bare-metal/on-premise infra**, simulating a **real-world enterprise environment**.  

---

## 🛠️ Project Evolution

### 1️⃣ Development Phase
- Built a raw **MERN TODO app** (frontend + backend).  
- Connected to **MongoDB**.  
- Verified app in **dev mode**.  

### 2️⃣ Dockerization
- Backend → Dockerized with **Node.js**, connected to MongoDB.  
- Frontend → Dockerized **React app with NGINX reverse proxy**.  
- Created a **custom Docker network** for service communication.  
- Used **Docker Compose** for multi-service orchestration.  
- Persistent storage via **volumes** for MongoDB.  

### 3️⃣ Kubernetes Migration
- Set up a **kubeadm cluster** (1 master + 1 worker).  
- Deployed frontend, backend, MongoDB with **manifests**.  
- Migrated MongoDB into a **StatefulSet** with:
  - Headless Service  
  - PersistentVolume (PV) & PersistentVolumeClaim (PVC)  
- Ensured **data persistence** across pod restarts.  

### 4️⃣ Observability & Load Testing
- Load-tested with **Apache Benchmark (ab)**.  
- Integrated **Prometheus + Grafana** (via Helm).  
- Observed **CPU/memory spikes** with increasing users.  

### 5️⃣ Networking & Load Balancing
- Deployed **MetalLB** for LoadBalancer IP assignment.  
- Configured **NGINX Ingress Controller** for routing.  
- External access enabled via **LAN subnet dynamic IPs**.  

### 6️⃣ Security Enhancements
- Exposed application via **HTTPS** using **Cloudflared Tunnel** with a free domain.  
- Used **Kubernetes Secrets & ConfigMaps** for sensitive data.  
- Migrated **secrets management to HashiCorp Vault**.  

### 7️⃣ GitOps with ArgoCD
- Installed **ArgoCD** and connected to this repo.  
- Configured **Helm charts** for manifests.  
- Enabled **auto-sync** → cluster always matches GitHub state.  

### 8️⃣ CI/CD with Jenkins
**Jenkins pipeline stages:**
1. Checkout Code  
2. Build Docker Images (frontend + backend)  
3. Push Images to Docker Hub  
4. Update K8s Manifests with new image tags  
5. Commit & Push Changes back to GitHub (triggers ArgoCD sync)  

✅ **End result → Fully automated GitOps pipeline.**  

---

## 📂 Repository Structure
