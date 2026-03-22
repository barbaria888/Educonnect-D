---

# EduConnect K3s Deployment

This repository contains a **bash script** to deploy the **EduConnect application** on a local K3s Kubernetes cluster with **Ingress-NGINX**. It automates the setup of MongoDB, Backend, Frontend, and ingress routing for easy testing and development.

---

## 🚀 Features

* Automatic installation of **Ingress-NGINX** (if not already present)
* Patching Ingress service to **NodePort** for external access
* Deployments for:
  * **MongoDB**
  * **Backend API**
  * **Frontend Application**
* Automatic **Nginx-Ingress** setup
* Waits for all deployments to be ready
* Prints **access URLs** after deployment
---

## 📋 Prerequisites

* **K3s or kubeadm** installed on your machine
* **kubectl** configured and connected to the K3s cluster
* Bash shell (`#!/bin/bash`)
* YAML files present in the same directory:

  * `mongodb.yaml`
  * `backend.yaml`
  * `frontend.yaml`
  * `ingress.yaml`

---

## ⚡ Quick Deployment

1. Clone the repository:

```bash
git clone --branch=production https://github.com/Dhruvsahu1/Educonnect-D.git
cd Educonnect/infrastructure
```

2. Make the script executable:

```bash
chmod +x deploy.sh
```

3. Run the deployment:

```bash
./deploy.sh
```

---

## 🛠 How It Works

1. **Check kubectl connectivity** to ensure cluster access.
2. **Install ingress-nginx** if the namespace doesn’t exist.
3. **Patch ingress-nginx service** to NodePort to expose HTTP and HTTPS externally.
4. **Deploy MongoDB, Backend, and Frontend** via their respective YAML files.
5. **Deploy Ingress** for routing frontend and backend traffic.
6. **Wait for all deployments** to be ready.
7. **Display pod, service, and ingress status**.
8. **Print URLs** to access the application and API.

---

## 🌐 Accessing EduConnect

After deployment, access the application via your machine’s IP:

```text
Frontend (HTTP): http://<NODE_IP>:<NODEPORT_HTTP>/
Backend API: http://<NODE_IP>:<NODEPORT_HTTP>/api
Health Check: http://<NODE_IP>:<NODEPORT_HTTP>/health
```

* Replace `<NODE_IP>` with the IP printed by the script
* `<NODEPORT_HTTP>` is automatically assigned by Kubernetes

---

## ⚠️ Notes

* **LoadBalancer services do not work** on local K3s clusters. NodePort is required for external access.
* Ensure all YAML files are correctly configured with container images and ports.
* Ingress routing will only work if NodePort is properly patched.

---

## 📦 Files

| File            | Description                          |
| --------------- | ------------------------------------ |
| `deploy.sh`     | Main deployment script               |
| `mongodb.yaml`  | MongoDB deployment/service manifest  |
| `backend.yaml`  | Backend deployment/service manifest  |
| `frontend.yaml` | Frontend deployment/service manifest |
| `ingress.yaml`  | Ingress routing manifest             |

---

## 🔧 Troubleshooting

* **502 Bad Gateway** → Ensure NodePort is exposed and ingress controller pods are running.
* **Pods stuck in Pending** → Check node resources and pod logs.
* **Ingress unreachable** → Verify NodePort and that your firewall allows access.

---
