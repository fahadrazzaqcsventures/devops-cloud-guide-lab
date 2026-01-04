# Twelve-Factor App Principles

The Twelve-Factor App methodology is a set of best practices for building **modern, scalable, and maintainable cloud-native applications**. It is essential for DevOps engineers to understand these principles, as they directly affect deployment, scaling, and operational practices.

---

## 1. Why This Topic Matters

Following these principles ensures applications are:

* Portable across environments
* Easy to scale horizontally
* Suitable for CI/CD pipelines
* Easy to maintain and troubleshoot

In your home lab, adhering to these principles helps simulate real-world cloud scenarios.

---

## 2. The Twelve Factors

1. **Codebase** – One codebase tracked in version control with many deploys
2. **Dependencies** – Explicitly declare and isolate dependencies
3. **Config** – Store configuration in environment variables, not code
4. **Backing Services** – Treat external services (DB, caches, queues) as attached resources
5. **Build, Release, Run** – Strictly separate build and run stages
6. **Processes** – Execute the app as one or more stateless processes
7. **Port Binding** – Export services via port binding, not runtime injection
8. **Concurrency** – Scale out via process model
9. **Disposability** – Fast startup, graceful shutdown, tolerate crashes
10. **Dev/Prod Parity** – Keep development, staging, and production as similar as possible
11. **Logs** – Treat logs as event streams; centralize processing
12. **Admin Processes** – Run administrative/management tasks as one-off processes

---

## 3. Home Lab Mapping

* Use Docker containers to enforce **stateless processes**
* Store configs in **environment variables**
* Simulate external services using MinIO, PostgreSQL, Redis
* Test horizontal scaling with multiple containers
* Observe logs centrally in ELK or Prometheus/Grafana

---

## 4. You Should Now Clearly Understand

* Twelve-Factor principles **enable scalable, maintainable, cloud-native apps**
* Stateless processes simplify **scaling and resilience**
* Configuration via environment variables enables **flexible deployments**
* Your lab experiments will **enforce and test these principles** for each service

---

## Next Theory Topic

[**Application Configuration Patterns (env vars, config files, secrets)**](../14-application-configuration-patterns/README.md)