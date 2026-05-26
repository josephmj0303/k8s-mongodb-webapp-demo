# Application Architecture

This project demonstrates deployment of a 2-tier containerized application on Kubernetes.

---

# Components

## Frontend Application

- Containerized Node.js web application
- Exposed internally using Kubernetes Service
- Routed externally using NGINX Ingress

---

## MongoDB Database

- MongoDB deployment running inside Kubernetes
- Internal communication through ClusterIP Service
- Credentials managed using Kubernetes Secrets

---

## Kubernetes Resources Used

- Deployment
- Service
- ConfigMap
- Secret
- Ingress

---

# Architecture Flow

```text
User Browser
      │
      ▼
NGINX Ingress Controller
      │
      ▼
webapp-service (ClusterIP)
      │
      ▼
WebApp Pods
      │
      ▼
mongo-service (ClusterIP)
      │
      ▼
MongoDB Pods
```

---

# Networking

Ingress Host:

```text
app.192.168.56.10.nip.io
```

Ingress Controller:

```text
NGINX Ingress Controller
```

Application Access:

```text
http://app.192.168.56.10.nip.io:31289
```

---

# Secrets Management

MongoDB credentials are stored securely using Kubernetes Secrets.

Example:

```yaml
kind: Secret
```

---

# Configuration Management

Application configuration is managed using Kubernetes ConfigMaps.

Example:

```yaml
kind: ConfigMap
```

---

# Scalability

Deployments support horizontal scaling.

Example:

```yaml
replicas: 2
```

---

# Future Improvements

Possible production enhancements:

- HTTPS with cert-manager
- Persistent Volumes
- StatefulSet for MongoDB
- Horizontal Pod Autoscaler
- Monitoring with Prometheus & Grafana
- GitOps with ArgoCD
- CI/CD pipeline integration
