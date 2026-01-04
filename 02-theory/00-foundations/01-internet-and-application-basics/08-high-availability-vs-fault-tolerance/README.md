# High Availability vs Fault Tolerance

This document explains the difference between **High Availability (HA)** and **Fault Tolerance (FT)**—two concepts that are frequently confused but have very different cost, design, and operational implications.

Understanding this distinction is mandatory for senior DevOps, Cloud Architects, and SREs.

---

## 1. Why This Topic Matters

Many systems fail not because they lack tools, but because they were designed with **incorrect availability assumptions**.

Common mistakes:

* Assuming HA means zero downtime
* Overengineering fault tolerance unnecessarily
* Underestimating cost and complexity

Senior principle:

> Availability is a business decision, not a technical default.

---

## 2. High Availability (HA)

### Definition

**High Availability** is the ability of a system to:

* Remain operational most of the time
* Recover quickly from failures

HA focuses on **minimizing downtime**, not eliminating it.

---

### Characteristics of HA Systems

* Redundancy (multiple instances)
* Automated failover
* Load balancing
* Monitoring and alerting

Typical downtime still exists, but it is **short and controlled**.

---

### Examples of HA

* Web servers behind a load balancer
* Multi-node Kubernetes clusters
* Databases with replicas

---

## 3. Fault Tolerance (FT)

### Definition

**Fault Tolerance** is the ability of a system to:

* Continue operating **without any interruption** when a component fails

FT assumes failures and absorbs them invisibly.

---

### Characteristics of FT Systems

* Active-active components
* No service interruption
* Duplicate everything
* Extremely high cost

FT systems aim for **zero downtime**.

---

### Examples of FT

* Aircraft control systems
* Medical life-support systems
* Financial trading engines

Most web applications do **not** need full fault tolerance.

---

## 4. HA vs FT (Comparison)

| Aspect      | High Availability   | Fault Tolerance          |
| ----------- | ------------------- | ------------------------ |
| Downtime    | Small, acceptable   | None                     |
| Cost        | Moderate            | Extremely high           |
| Complexity  | Manageable          | Very high                |
| Typical Use | Web & cloud systems | Mission-critical systems |

---

## 5. Failure Handling Differences

### HA Failure Scenario

* Instance crashes
* Load balancer reroutes traffic
* Brief disruption possible

### FT Failure Scenario

* Component fails
* Duplicate component takes over instantly
* Users never notice

DevOps reality:

> Most DevOps systems are **highly available**, not fault tolerant.

---

## 6. Cloud Perspective

Cloud providers enable HA easily:

* Multiple availability zones
* Managed load balancers
* Auto Scaling Groups

True fault tolerance in the cloud is:

* Rare
* Very expensive
* Often unnecessary

---

## 7. Kubernetes Perspective

In Kubernetes:

* Deployments provide HA
* ReplicaSets replace failed Pods
* Nodes can fail with brief impact

Kubernetes is **not fault tolerant** by default.

---

## 8. Measuring Availability

Availability is measured as:

```
Availability (%) = (Uptime / Total Time) × 100
```

Examples:

* 99.9% ("three nines") ≈ 8.7 hours downtime/year
* 99.99% ("four nines") ≈ 52 minutes downtime/year

Higher availability exponentially increases cost.

---

## 9. Home Lab Mapping

In your lab:

* Single Proxmox host → No HA
* Multiple VMs → HA patterns
* Kubernetes replicas → HA

You will simulate:

* Node failures
* Pod crashes
* Load balancer rerouting

---

## 10. Interview-Grade Takeaways

* HA minimizes downtime; FT eliminates it
* Most systems require HA, not FT
* Availability targets must align with business needs
* Design for failure, not perfection

---

## You should be able to explain clearly:

* Why most DevOps platforms are HA, not FT
* Why “zero downtime” is usually a business myth
* How cost increases non-linearly with availability targets
* Why Kubernetes ≠ fault tolerance

---

## Next Topic

Proceed to:
[**Scalability vs Elasticity**](../09-scalability-vs-elasticity/README.md)
