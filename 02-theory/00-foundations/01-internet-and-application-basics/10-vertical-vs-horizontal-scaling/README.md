# Vertical vs Horizontal Scaling

This document explains **Vertical Scaling** and **Horizontal Scaling**, providing clarity on how resources are adjusted to handle workloads.

Understanding this is critical for both home lab exercises and real-world cloud architectures.

---

## 1. Definitions

* **Vertical Scaling (Scale-Up):**

  * Adding more power (CPU, RAM, storage) to an existing server or VM.
  * Example: Upgrading a VM from 4GB RAM / 2 CPUs to 16GB RAM / 8 CPUs.

* **Horizontal Scaling (Scale-Out):**

  * Adding more instances of servers or containers to distribute load.
  * Example: Adding additional web servers behind a load balancer.

---

## 2. Key Characteristics

| Aspect          | Vertical Scaling        | Horizontal Scaling                               |
| --------------- | ----------------------- | ------------------------------------------------ |
| Implementation  | Upgrade single machine  | Add more machines/instances                      |
| Downtime        | Possible during upgrade | Minimal, often seamless                          |
| Complexity      | Low                     | Higher (requires load balancing & orchestration) |
| Cost Efficiency | Limited by hardware     | Can scale indefinitely                           |
| Use Case        | Monoliths, databases    | Stateless applications, microservices            |

---

## 3. Pros & Cons

**Vertical Scaling:**

* Pros: Simpler, less network complexity, easier to manage
* Cons: Limited by hardware, potential downtime, single point of failure

**Horizontal Scaling:**

* Pros: Supports redundancy, high availability, almost limitless scaling
* Cons: Requires orchestration, load balancing, more complex monitoring

---

## 4. Home Lab Mapping

* **Vertical Scaling Experiments:**

  * Increase RAM/CPU of Proxmox VM and monitor performance
* **Horizontal Scaling Experiments:**

  * Deploy multiple VMs running the same service behind Nginx reverse proxy
  * Observe load distribution and test failure recovery

These experiments prepare you for **Kubernetes replicas, cloud auto-scaling, and HA systems**.

---

## 5. You Should Now Clearly Understand

* Vertical scaling increases **resources per machine**; horizontal scaling increases **number of machines**
* Vertical scaling is simpler but limited; horizontal scaling is complex but more resilient and scalable
* Horizontal scaling is key for cloud-native, microservices, and highly available architectures
* Your home lab will let you **see performance and failure effects of both strategies**

---

## Next Theory Topic

[**Application Support and Maintenance**](../11-application-support-and-maintenance/README.md)
