# NavyBattle.Net

## Tech Demo - Incomplete

This is a tech demo using Kubernetes and ASP.NET Core

🚩This entire project is currently under development


## Setup - Container images

🚩TODO

## Setup - Quick Ubuntu Demo

### Requirements

This setup will require
- A domain name
- A fresh Ubuntu 24.04 (LTS) instance 
- With at least 1GB Memory (2GB recommended)
- A container registry with NavyBattle.Net container images built 
(From earlier step)
- Your contact email for Let's Encrypt setup 

### Setup domain records

Create an A-Record for your domain (or subdomain) pointing to your instance public ip

### Configure firewall

Enable ssh, http and https

```bash
ufw allow 22   # SSH
ufw allow 80   # HTTP
ufw allow 443  # HTTPS
ufw enable
```

### Install k3s
This is a lightweight kubernetes distribution

Installation can take up to 30s

```bash
curl -sfL https://get.k3s.io | sh - 
```

Check the status

```bash
k3s kubectl get node  
```

### Install Certmanager

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.12.0/cert-manager.yaml
```

### Clone repo

```bash
apt-get update
apt-get install git -y
git clone https://github.com/sleepyparadox/navybattle.net.git /var/navybattle.net
```

### Edit repo

Edit `k8s/common/cluster-issuer.yaml`

| Replace | With |
|---|---|
|me@example.com| Your email |


Edit `k8s/base/navybattle-ingress.yaml`

| Replace | With |
|---|---|
|navybattle.net| Your email |


### Deploy cluster

```bash
kubectl apply -f k8s/common/cluster-issuer.yaml
kubectl apply -f k8s/base/navybattle-api.yaml
kubectl apply -f k8s/base/navybattle-ingress.yaml
```
