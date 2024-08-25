# NavyBattle.Net

## Tech Demo - Incomplete

This is a tech demo using Kubernetes and ASP.NET Core

🚩This entire project is currently under development


## Setup - Container images

🚩TODO

## Setup - Quick Ubuntu Demo

#### Requirements

This setup will require
- A domain name
- A fresh Ubuntu 24.04 (LTS) instance 
- With at least 1GB Memory (2GB recommended)
- A container registry with NavyBattle.Net container images built 
(From earlier step)

#### Setup domain records

Create an A-Record for your domain (or subdomain) pointing to your instance public ip

#### Install k3s
This is a lightweight kubernetes distribution

Installation can take up to 30s

```bash
curl -sfL https://get.k3s.io | sh - 
```

Check the status

```bash
k3s kubectl get node  
```
#### Clone repo

```bash
apt-get update
apt-get install git -y
sudo mkdir -p /var/navybattle.net
git clone https://github.com/sleepyparadox/navybattle.net.git /var/navybattle.net
```

#### Configure resources for your domain

`k8s/common/cluster-issuer.yaml`

| Replace | With | Note
|---|---|---|
|me@example.com| Your email | This is the email used with the Let's Encrypt cert authority |

`k8s/base/navybattle-cert.yaml`

| Replace | With | Note
|---|---|---|
|navybattle.net| Your domain | This domain will receive a https cert |

`k8s/base/navybattle-ingress.yaml`

| Replace | With | Note
|---|---|---|
|navybattle.net| Your domain | This domain will have ingress from the internet |



#### Install certmanager

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.12.0/cert-manager.yaml
```

Edit k8s/common/letsencrypt.yaml

Replace your-email@example.com with your email

```bash
kubectl apply -f k8s/common/letsencrypt.yaml
```

```bash
k3s kubectl get node  
```

#### Setup cluster

Create navybattle.net
