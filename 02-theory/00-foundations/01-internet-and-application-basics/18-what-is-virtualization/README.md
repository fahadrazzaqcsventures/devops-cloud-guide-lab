# What is Virtualization

This document introduces **virtualization**, a foundational concept for DevOps, cloud computing, and modern infrastructure platforms such as Proxmox, VMware, and public clouds.

Virtualization is the bridge between **physical hardware** and **flexible, software-defined infrastructure**.

---

## 1. Why This Topic Matters

Without virtualization:

* Cloud computing would not exist
* Infrastructure would be slow to provision
* Environments would be tightly coupled to hardware

Every DevOps engineer must deeply understand virtualization before working with containers, Kubernetes, or cloud platforms.

---

## 2. What Is Virtualization?

**Virtualization** is the abstraction of physical hardware resources (CPU, memory, storage, network) into **logical, software-defined resources**.

It allows:

* Multiple isolated systems to run on one physical machine
* Better hardware utilization
* Faster provisioning and recovery

---

## 3. Problems Virtualization Solves

Before virtualization:

* One OS per physical server
* Low utilization (5–15%)
* Long provisioning times
* Hardware-dependent deployments

After virtualization:

* Multiple VMs per host
* High utilization (60–80%)
* Rapid provisioning
* Hardware abstraction

---

## 4. Core Virtualization Concepts

* **Host**: Physical machine running the virtualization layer
* **Guest**: Virtual machine running inside the host
* **Hypervisor**: Software that manages VMs
* **Virtual CPU (vCPU)**: Abstracted CPU resource
* **Virtual NIC**: Software-defined network interface
* **Virtual Disk**: File-backed or block-backed storage

---

## 5. Virtualization vs Containers (High-Level)

| Aspect    | Virtual Machines | Containers            |
| --------- | ---------------- | --------------------- |
| OS        | Full OS per VM   | Shared host kernel    |
| Isolation | Strong           | Lighter               |
| Boot Time | Minutes          | Seconds               |
| Use Case  | Infrastructure   | Application packaging |

Containers still depend on virtualization at scale (cloud, Kubernetes nodes).

---

## 6. Home Lab Mapping

In your lab:

* Proxmox host = virtualization platform
* VMs = simulated cloud instances (EC2-like)
* Virtual networks = VPC-like isolation

You will intentionally:

* Overcommit resources
* Kill VMs
* Rebuild environments

---

## 7. You Should Now Clearly Understand

* Virtualization abstracts physical hardware into software-defined resources
* It enables cloud computing, HA, and fast recovery
* VMs are the foundation beneath containers and Kubernetes
* Proxmox is your practical virtualization control plane

---

## Next Theory Topic

[**What is a Hypervisor**](../19-what-is-hypervisor/README.md)