# Home Lab Architecture

This document defines the **formal architecture** of the home lab used to practice DevOps, Cloud, SRE, and Platform Engineering concepts. It is intentionally written in a **production-style format** suitable for portfolio and interview discussion.

---

## 1. PURPOSE & DESIGN PRINCIPLES

### Purpose

The home lab simulates a **small production environment** to practice:

* Linux system administration
* Networking and security
* Automation and CI/CD
* Infrastructure as Code
* Containerization and Kubernetes
* Observability, reliability, and incident response

### Design Principles

* Reproducibility over permanence
* Failure-driven learning
* Minimal hardware, maximal learning
* Clear separation of responsibilities
* Documentation-first mindset

---

## 2. HARDWARE INVENTORY

### Control Machine

* Personal laptop (daily use)
* Role: CLI access, Git, Terraform, kubectl, dashboards

### Lab Compute

#### Proxmox Host (Primary)

* CPU: Intel i5 (3rd generation)
* RAM: 8 GB
* Storage: 500 GB HDD
* Hypervisor: Proxmox VE
* Architecture: x86_64

#### Raspberry Pi 3 B+ (Edge Node)

* CPU: ARM
* RAM: 1 GB
* Storage: SD card
* Role: always-on edge and utility services

---

## 3. HIGH-LEVEL ARCHITECTURE

```
[ Personal Laptop ]
        |
        | SSH / HTTPS / VPN
        |
[ Proxmox Host ]----------------[ Raspberry Pi ]
        |
        | Proxmox Bridge (vmbr0)
        |
   [ Virtual Machines ]
```

The lab emulates a **mini data center** with centralized compute and an edge services node.

---

## 4. NETWORK ARCHITECTURE

### Network Segments

| Network      | CIDR           | Purpose             |
| ------------ | -------------- | ------------------- |
| LAN          | 192.168.1.0/24 | Physical network    |
| LAB-MGMT     | 10.0.0.0/24    | VM management & SSH |
| LAB-SERVICES | 10.0.1.0/24    | Application traffic |

### Proxmox Networking

* `vmbr0` → LAN (NAT / bridge)
* `vmbr1` → LAB-MGMT (internal)
* `vmbr2` → LAB-SERVICES (internal)

### DNS Strategy

* Raspberry Pi runs DNS (Pi-hole or CoreDNS)
* All VMs use Pi as primary DNS

### Failure Scenarios

* DNS outage
* Incorrect routing
* Firewall misconfiguration

---

## 5. VIRTUAL MACHINE INVENTORY

| VM Name       | RAM  | CPU | Network    | Purpose                  |
| ------------- | ---- | --- | ---------- | ------------------------ |
| linux-core-01 | 1G   | 1   | MGMT       | Linux fundamentals       |
| cicd-runner   | 1.5G | 2   | MGMT       | Jenkins / runners        |
| k8s-control   | 2G   | 2   | MGMT + SRV | Kubernetes control plane |
| k8s-worker-01 | 2G   | 2   | SRV        | Kubernetes workloads     |
| monitoring    | 1.5G | 1   | SRV        | Prometheus / Grafana     |

All VMs run **Ubuntu Server LTS** with minimal packages.

---

## 6. RASPBERRY PI ROLE (EDGE SERVICES)

### Services Hosted

* DNS (Pi-hole / CoreDNS)
* Reverse proxy (Nginx)
* VPN endpoint (WireGuard)
* Node exporter

### Rationale

* Always-on node
* ARM + x86 heterogeneity
* Edge-service simulation

---

## 7. ENVIRONMENT SEPARATION

Logical environments are separated by:

* Namespace (Kubernetes)
* Git branches
* Terraform workspaces

| Environment | Purpose                |
| ----------- | ---------------------- |
| dev         | Experimentation        |
| stage       | Pre-production testing |
| prod        | Stable baseline        |

---

## 8. SECURITY MODEL

### Access

* SSH key-based authentication
* No password SSH
* Separate users per role

### Network Security

* Default deny firewall rules
* Explicit port opening
* Internal-only services

### Secrets Management

* Environment variables (early)
* SOPS / sealed-secrets (later)

---

## 9. BACKUP & RECOVERY STRATEGY

### Backup Scope

* Git repositories (remote)
* VM snapshots (selective)
* Kubernetes manifests

### Recovery Philosophy

* Rebuild > restore
* Infrastructure recreated via code

### Failure Scenarios

* Disk failure
* Accidental destroy
* State corruption

---

## 10. OBSERVABILITY STRATEGY

### Metrics

* Node exporter
* Kubernetes metrics

### Logs

* Application logs
* System logs

### Alerts

* Node down
* High resource usage
* Pod crash loops

---

## 11. INFRASTRUCTURE AS CODE STRATEGY

### Tools

* Terraform (Proxmox provider)
* Ansible

### Goals

* Repeatable lab rebuild
* Environment parity
* Change traceability

---

## 12. FAILURE INJECTION PLAN

Intentional failures include:

* Killing core services
* Breaking DNS
* Resource starvation
* Network isolation
* Credential revocation

Each failure requires:

* Detection
* Root cause analysis
* Fix
* Documentation

---

## 13. DOCUMENTATION STANDARDS

Every component must have:

* Purpose
* Architecture diagram
* Failure modes
* Recovery steps

Documentation is stored in GitHub alongside code.

---

## 14. EVOLUTION PLAN

Phase-based growth:

* Start: Linux, Docker, CI/CD
* Mid: Kubernetes, IaC
* Advanced: GitOps, SRE, AIOps

Hardware upgrades are optional, not required.

---

## 15. SUCCESS CRITERIA

This lab is successful if you can:

* Destroy and rebuild it confidently
* Explain every design decision
* Debug failures under pressure
* Use it as evidence of senior-level thinking
