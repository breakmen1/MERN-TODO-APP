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
├── backend/ # Node.js backend

├── frontend/ # React frontend

├── nginx/ # Nginx reverse proxy configs

├── docker-compose.yml # Multi-container setup

├── k8s-manifest/ # Kubernetes manifests

│ ├── backend-deployment.yml

│ ├── backend-service.yml

│ ├── frontend-deployment.yml

│ ├── frontend-service.yml

│ ├── mongo-statefulset.yaml

│ ├── mongo-pv-0.yaml

│ ├── mongo-headless-service.yaml
│ ├── ingress-nginx-svc.yaml

│ └── metallb-config.yaml

├── Jenkinsfile # CI/CD pipeline definition

└── README.md # Project documentation



---

## 🔧 CI/CD Pipeline (Jenkinsfile)

### Pipeline Flow
1. **Checkout Code** → Pull latest repo changes.  
2. **Build Images** → Frontend & Backend images built with tags (`:build_number`).  
3. **Push to Docker Hub** → Images pushed with version tag.  
4. **Update K8s Manifests** → Replace old image versions with new build tag.  
5. **Commit & Push to GitHub** → Repo updated → ArgoCD auto-syncs cluster.  

✅ **Result → GitHub repo always in sync with running Kubernetes cluster.**  

---

## 📊 Tools & Technologies
- **Application Layer:** MERN (MongoDB, Express.js, React, Node.js)  
- **Containerization:** Docker, Docker Compose  
- **Orchestration:** Kubernetes (kubeadm cluster)  
- **Networking:** MetalLB, NGINX Ingress Controller  
- **Monitoring:** Prometheus + Grafana  
- **Security:** Kubernetes Secrets, ConfigMaps, HashiCorp Vault  
- **CI/CD:** Jenkins, ArgoCD, GitHub  
- **Other:** Cloudflared Tunnel for HTTPS  

---

## 🌐 Final Architecture
```mermaid
flowchart LR
    User((User)) --> Ingress[NGINX Ingress Controller]
    Ingress --> ALB[MetalLB LoadBalancer]
    ALB --> Frontend[React + Nginx Pod]
    Frontend --> Backend[Node.js Pod]
    Backend --> DB[(MongoDB StatefulSet)]


**Outcome:**

End-to-End CI/CD for MERN app.
GitOps-enabled → Cluster state always reflects GitHub repo.
Scalable & Secure Deployment on self-hosted Kubernetes.
Hands-on exposure to real-world DevOps challenges.


**Key Takeaways:**

Deep dive into Docker, Kubernetes, Jenkins, ArgoCD.
Learned troubleshooting & debugging real-world issues.
Built a production-grade CI/CD pipeline from scratch.
