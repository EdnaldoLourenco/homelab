## Overview
This project demonstrates a production-like Kubernetes homelab using a multi-node k3s cluster built on Proxmox, focused on observability, persistent storage, and real-world troubleshooting.

This project is continuously evolving.

## Hardware & Virtualization

**Host:** Dell OptiPlex 3050 (Intel Core i3-7100T, 2C/4T)  
**RAM:** 20 GB  
**SSD:** 500GB  
**Virtualization:** Proxmox VE

### Virtual Machines
This homelab runs a multi-node k3s cluster on 3 Ubuntu VMs:

| VM | Role | vCPU | RAM | Disk | Notes |
|---|---|---:|---:|---:|---|
| k3s | control-plane | 2 | 7 GB | 60+ GB | runs control-plane workloads |
| k3s-worker1 | worker | 1 | 6 GB | 60+ GB | worker node |
| k3s-worker2 | worker | 1 | 5 GB | 60+ GB | worker node |


## Cluster Provisioning

### OS & Kubernetes
- Ubuntu 24.04 LTS on all nodes
- k3s (multi-node cluster)
- containerd runtime

### Networking
- Internal IP range: `10.0.0.0/24` (homelab LAN)
- Ingress Controller: Traefik (installed via Helm)
- Local DNS: `*.lab.local` (hosts file / local DNS setup)

### Storage
- Longhorn as default StorageClass
- PVC-backed workloads for stateful components (Grafana, Prometheus, Loki, PostgreSQL)

### Observability
- kube-prometheus-stack (Prometheus + Grafana)
- Loki + Promtail for centralized logs
- Metrics scraped via ServiceMonitor

### Databases
- PostgreSQL installed via Helm with Prometheus metrics enabled
- Access via pgAdmin (web UI)

## Key Features
- Multi-node Kubernetes cluster
- Persistent workloads with Longhorn
- Centralized logging and metrics
- Ingress with Traefik
- PostgreSQL with persistent storage

## Challenges & Solutions
- Longhorn replica scheduling failures
- Grafana PVC recovery
- ServiceMonitor recreation
- Loki memory tuning