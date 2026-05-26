# NGINX Ingress Setup

This document explains how Ingress was configured for domain-based access inside a Vagrant Kubernetes environment.

---

# Why Ingress

Instead of accessing the application using:

```text
http://NODE-IP:NODEPORT
```

Ingress provides:

- Domain-based routing
- Cleaner URLs
- Reverse proxy support
- Better production-style architecture

Example:

```text
http://app.192.168.56.10.nip.io:31289
```

---

# Install NGINX Ingress Controller

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

Verify:

```bash
kubectl get pods -n ingress-nginx
```

---

# Verify Ingress Controller Service

```bash
kubectl get svc -n ingress-nginx
```

Example:

```text
ingress-nginx-controller   LoadBalancer   10.x.x.x   <pending>   80:31289/TCP
```

Since this setup runs on Vagrant/bare-metal, EXTERNAL-IP remains pending.

Traffic is exposed through NodePort.

---

# Ingress Resource

Example ingress configuration:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: webapp-ingress

spec:
  ingressClassName: nginx

  rules:
  - host: app.192.168.56.10.nip.io
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: webapp-service
            port:
              number: 3000
```

Apply:

```bash
kubectl apply -f ingress.yaml
```

---

# Verify Ingress

```bash
kubectl get ingress
```

Expected output:

```text
NAME             CLASS   HOSTS
webapp-ingress   nginx   app.192.168.56.10.nip.io
```

---

# Access Application

```text
http://app.192.168.56.10.nip.io:31289
```

---

# Using nip.io

nip.io is a wildcard DNS service.

It automatically maps:

```text
app.192.168.56.10.nip.io
```

to:

```text
192.168.56.10
```

Benefits:

- No /etc/hosts editing
- No DNS server required
- Ideal for Kubernetes labs and demos

---

# Troubleshooting

Check ingress:

```bash
kubectl describe ingress webapp-ingress
```

Check ingress controller:

```bash
kubectl get pods -n ingress-nginx
```

Check service endpoints:

```bash
kubectl get endpoints
```

Check NodePort:

```bash
kubectl get svc -n ingress-nginx
```
