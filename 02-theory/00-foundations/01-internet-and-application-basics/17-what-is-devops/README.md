# What is DevOps (Culture, Feedback Loops, Ownership)

This document defines **DevOps** as a culture and operating model—not a set of tools. Understanding this is essential to correctly applying everything you have studied so far.

---

## 1. Why This Topic Matters

Many engineers misunderstand DevOps as:

* CI/CD tools
* Cloud platforms
* Automation scripts

In reality, DevOps is about **how teams work**, **how feedback flows**, and **who owns reliability**.

---

## 2. Definition of DevOps

**DevOps** is a set of cultural principles and practices that:

* Shorten feedback loops between development and operations
* Improve deployment frequency and reliability
* Establish clear ownership of systems in production

DevOps optimizes for **speed with stability**, not speed alone.

---

## 3. Core Pillars of DevOps

### 3.1 Culture

* Shared responsibility for production
* Blameless postmortems
* Continuous learning from incidents

> "You build it, you run it" is a DevOps principle.

---

### 3.2 Automation

* CI/CD pipelines
* Infrastructure as Code
* Self-healing systems

Automation reduces human error and increases repeatability.

---

### 3.3 Measurement

* Deployment frequency
* Lead time for changes
* Mean Time To Recovery (MTTR)
* Change failure rate

What you measure influences behavior.

---

### 3.4 Sharing

* Documentation
* Runbooks
* Knowledge transfer

Sharing reduces single points of failure (people).

---

## 4. Feedback Loops

Fast feedback is central to DevOps:

* Code commit → CI feedback
* Deployment → Monitoring alerts
* Incident → Postmortem → Process improvement

The shorter the loop, the safer the change.

---

## 5. Ownership Model

* DevOps teams **own services end-to-end**
* Ownership includes:

  * Deployment
  * Monitoring
  * Incident response
  * Continuous improvement

This is why DevOps engineers participate in on-call rotations.

---

## 6. Home Lab Mapping

In your lab you will:

* Own services from build to failure
* Trigger incidents intentionally
* Respond, document, and improve systems

Your lab is designed to simulate **real DevOps ownership**, not just deployments.

---

## 7. You Should Now Clearly Understand

* DevOps is a **culture and operating model**, not tooling
* Fast feedback loops reduce risk
* Ownership of production is non-negotiable
* Your lab is structured around **build → break → respond → document**

---

## Next Theory Topic

[**What is Virtualization**](../18-what-is-virtualization/README.md)
