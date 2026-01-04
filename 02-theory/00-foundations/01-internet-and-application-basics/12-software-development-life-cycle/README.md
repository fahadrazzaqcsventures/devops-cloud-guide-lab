# Software Development Life Cycle (SDLC)

This document explains the **Software Development Life Cycle (SDLC)** and its relevance to DevOps and operational practices.

SDLC is the process that defines **how software is conceived, built, tested, and maintained**. Understanding it is essential for seamless collaboration between development and operations.

---

## 1. Why This Topic Matters

DevOps exists to bridge development and operations. Understanding SDLC:

* Provides context for deployment and incident response
* Guides automation and CI/CD pipeline design
* Enables better collaboration with developers

---

## 2. Common SDLC Models

1. **Waterfall Model:** Sequential, rigid phases. Rarely used in modern DevOps.
2. **Iterative Model:** Develop in cycles, review and improve.
3. **Agile Model:** Incremental development, feedback-driven.
4. **DevOps Model:** Continuous integration, continuous delivery, and continuous feedback.

> DevOps aligns most closely with Agile + Continuous Delivery principles.

---

## 3. Typical SDLC Phases

| Phase          | Description                    | DevOps Relevance                                                |
| -------------- | ------------------------------ | --------------------------------------------------------------- |
| Requirements   | Gather business needs          | Ensures observability and reliability requirements are included |
| Design         | Architecture & planning        | Guides infrastructure, scaling, and HA decisions                |
| Implementation | Coding                         | Enables version control and CI/CD integration                   |
| Testing        | Unit, integration, system      | Automated testing pipelines, QA environments                    |
| Deployment     | Release to production          | Continuous delivery, blue/green, canary deployments             |
| Maintenance    | Updates, monitoring, bug fixes | Observability, incident response, patch management              |

---

## 4. DevOps Integration Points

* **Version Control:** Git repositories track code and infra-as-code
* **CI/CD Pipelines:** Automate build, test, deployment
* **Monitoring:** Feedback loop to detect failures and improve the system
* **Incident Management:** Postmortems feed back into SDLC

---

## 5. Home Lab Mapping

* Simulate SDLC by:

  * Implementing code changes in your lab VMs
  * Deploying via scripts or GitHub Actions
  * Observing logs, metrics, and incident response
* Document each phase in your portfolio repo

---

## 6. You Should Now Clearly Understand

* SDLC is the backbone of **software planning, implementation, and maintenance**
* DevOps overlays SDLC with **automation, feedback, and reliability**
* Each phase of SDLC is a potential **failure point**, which your lab exercises will expose
* Knowing SDLC helps you **integrate theory with lab practice**

---

## Next Theory Topic

[**Twelve-Factor App Principles**](../14-application-configuration-patterns/README.md)
