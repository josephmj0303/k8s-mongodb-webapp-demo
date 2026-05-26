# Kubernetes MongoDB WebApp Setup

This project demonstrates deployment of a simple 2-tier application on Kubernetes using:

- MongoDB
- Kubernetes Deployments
- Services
- ConfigMaps
- Secrets
- NGINX Ingress Controller

The application is deployed inside a Vagrant-based Kubernetes cluster.

---

# Prerequisites

- VirtualBox
- Vagrant
- kubectl
- Kubernetes cluster
- NGINX Ingress Controller

---

# Project Structure

```text
k8s-ingress-mongo-webapp-demo/
│
├── architecture/
│   └── architecture-diagram.png
│
├── kubernetes/
│   ├── mongo-secret.yaml
│   ├── mongo-config.yaml
│   ├── mongo.yaml
│   ├── webapp.yaml
│   └── ingress.yaml
│
├── docs/
│   ├── setup.md
│   ├── ingress-setup.md
│   └── architecture.md
│
├── screenshots/
│
└── README.md
```

---

# Deploy MongoDB Secret

```bash
kubectl apply -f mongo-secret.yaml
```

---

# Deploy ConfigMap

```bash
kubectl apply -f mongo-config.yaml
```

---

# Deploy MongoDB

```bash
kubectl apply -f mongo.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
```

---

# Deploy Web Application

```bash
kubectl apply -f webapp.yaml
```

Verify:

```bash
kubectl get pods
kubectl get svc
```

---

# Deploy Ingress

```bash
kubectl apply -f ingress.yaml
```

Verify:

```bash
kubectl get ingress
```

---

# Access Application

Example:

```text
http://app.192.168.56.10.nip.io:31289
```

---

# Useful Commands

Check pods:

```bash
kubectl get pods
```

Check services:

```bash
kubectl get svc
```

Check ingress:

```bash
kubectl get ingress
```

View logs:

```bash
kubectl logs <pod-name>
```

Describe resource:

```bash
kubectl describe pod <pod-name>
```

---

# Cleanup

```bash
kubectl delete -f .
```
