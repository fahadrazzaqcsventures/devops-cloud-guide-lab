# DevOps Cloud Guide + Home Lab

Welcome to the **DevOps Cloud Guide Lab** — a comprehensive, hands-on roadmap designed to take you from **zero experience to senior DevOps and Cloud Architect level**. This repository combines structured theory, practical labs, failure-driven exercises, and decision documentation.

---

## Repository Overview

This repository is organized to reflect a **progressive, production-oriented learning path**:

### 1. `roadmap/`

Contains the complete **DevOps → Senior Cloud Architect roadmap**, defining the topics and skills you need to master. Use this to understand **what to learn next and how concepts connect**.

### 2. `theory/`

All conceptual learning materials:

* Internet, applications, OS fundamentals
* Networking, ports, load balancing
* Automation, scripting, containerization
* Cloud fundamentals, CI/CD, observability

**Recommendation:** Read each theory file **before performing corresponding lab exercises**.

### 3. `home-lab/`

Week-by-week lab instructions:

* Step-by-step build tasks
* Failure injection scenarios
* Portfolio outputs

### 4. `home-lab-architecture/`

Document and diagrams describing your **hardware setup**, network design, and virtualization architecture. Study this before starting any labs to understand your lab’s infrastructure.

### 5. `devops-home-lab-master-plan/`

The **master plan** combining all theory, labs, and incidents. Use this as a **central guide** to coordinate your learning, practice, and documentation.

### 6. `incident-response-playbooks/`

Step-by-step **playbooks for all common failure types**, from Linux services to Kubernetes, CI/CD, networking, and storage. **Break, respond, and recover using these playbooks**.

### 7. `weekly-incident-response-mapping/`

Maps **incident playbooks to each week** of your home lab plan. Before each lab week, review relevant incidents to prepare for failure-driven exercises.

### 8. `adr-templates/`

Document your design decisions to build a **senior-level portfolio**:

* **Basic ADR** — general decisions
* **Week-Specific ADR** — tied to home lab weeks
* **Cloud/IaC ADR** — Terraform, Ansible, cloud resources

---

## Learning Workflow

Every week follows the **production-oriented learning loop**:

1. **Theory** — study the relevant concepts in `theory/` and refer to `roadmap/` for context.
2. **Build** — perform the lab for the week in `home-lab/` following the master plan.
3. **Break** — intentionally inject failures as described in the lab and playbooks.
4. **Respond** — use `incident-response-playbooks/` and weekly mappings to recover.
5. **Document** — create ADRs (`adr-templates/`) and portfolio artifacts (screenshots, scripts, YAMLs, diagrams).

**Portfolio-Driven Mindset:** Every lab week should leave you with **tangible, version-controlled assets** demonstrating operational and architectural skills.

---

## Recommended Execution Order

1. Review `home-lab-architecture/` to understand your environment.
2. Start with **PHASE 0: Foundations** (Week 1–4), reading theory first.
3. Progress **week by week**:

   * `theory/` → `home-lab/` → break failures → respond → document ADRs.
4. Use `devops-home-lab-master-plan/` to track your progress and dependencies.
5. Reference `incident-response-playbooks/` and `weekly-incident-response-mapping/` to guide recovery exercises.
6. After completing PHASE 1–F, ensure all `ADRs`, playbooks, and lab outputs are **versioned and organized** in the repository.

---

## Expected Outcomes

By completing this repository:

* Master Linux, networking, automation, containerization, CI/CD, Kubernetes, GitOps, cloud fundamentals, observability, and SRE practices.
* Have a **home lab portfolio** demonstrating practical experience.
* Be able to **document, analyze, and justify architectural decisions** using ADRs.
* Develop a **failure-driven operational mindset**, essential for senior DevOps and cloud roles.

---

## Notes

* Do **not skip failure exercises**; senior expertise comes from recovery experience.
* Maintain consistent **Git commits** for all scripts, configs, ADRs, and diagrams.
* Review roadmap periodically to identify gaps in theory or lab experience.
* Use this repository as a **living, evolving guide**, not a static resource.
