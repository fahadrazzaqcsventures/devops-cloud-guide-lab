# DevOps & Cloud Roadmap (Beginner → Senior)

This roadmap is designed to take you from **absolute beginner** to **senior DevOps engineer / cloud architect**, without removing any original topics and with added senior-level improvements.

---

## PHASE 0: FOUNDATIONS — INTERNET, APPLICATIONS & SYSTEM THINKING

### Internet & Application Basics

* [How the internet works](../02-theory/00-foundations/01-internet-and-application-basics/01-how-the-internet-works/README.md)
* [What is a server](../02-theory/00-foundations/01-internet-and-application-basics/02-what-is-a-server/README.md)
* [What is an application](../02-theory/00-foundations/01-internet-and-application-basics/03-what-is-an-application/README.md)
* [Web server vs application server](../02-theory/00-foundations/01-internet-and-application-basics/04-web-server-vs-application-server/README.md)
* [Client–server architecture](../02-theory/00-foundations/01-internet-and-application-basics/05-client–server-architecture/README.md)
* [Stateless vs stateful systems](../02-theory/00-foundations/01-internet-and-application-basics/06-stateless-vs-stateful-systems/README.md)
* [Monolithic vs microservices architecture](../02-theory/00-foundations/01-internet-and-application-basics/07-monolithic-vs-microservices-architecture/README.md)
* [High availability vs fault tolerance](../02-theory/00-foundations/01-internet-and-application-basics/08-high-availability-vs-fault-tolerance/README.md)
* [Scalability vs elasticity](../02-theory/00-foundations/01-internet-and-application-basics/09-scalability-vs-elasticity/README.md)
* [Vertical vs horizontal scaling](../02-theory/00-foundations/01-internet-and-application-basics/10-vertical-vs-horizontal-scaling/README.md)
* [Application support and maintenance](../02-theory/00-foundations/01-internet-and-application-basics/11-application-support-and-maintenance/README.md)
* [Software Development Life Cycle (SDLC)](../02-theory/00-foundations/01-internet-and-application-basics/12-software-development-life-cycle/README.md)
* [Twelve-Factor App principles](../02-theory/00-foundations/01-internet-and-application-basics/13-twelve-factor-app-principles/README.md)
* [Application configuration patterns (env vars, config files, secrets](../02-theory/00-foundations/01-internet-and-application-basics/14-application-configuration-patterns/README.md)
* [Backend service flow (request → logic → DB → response)](../02-theory/00-foundations/01-internet-and-application-basics/15-backend-service-flow/README.md)
* [REST API fundamentals](../02-theory/00-foundations/01-internet-and-application-basics/16-rest-api-fundamentals/README.md)
* [What is DevOps (culture, feedback loops, ownership)](../02-theory/00-foundations/01-internet-and-application-basics/17-what-is-devops/README.md)
* [What is Virtualization](../02-theory/00-foundations/01-internet-and-application-basics/18-what-is-virtualization/README.md)
* [What is hypervisor](../02-theory/00-foundations/01-internet-and-application-basics/19-what-is-hypervisor/README.md)
* [Hypervisor types and architecture](../02-theory/00-foundations/01-internet-and-application-basics/20-hypervisor-types-and-architecture/README.md)
* [Proxmox control plane, storage, VM networking](../02-theory/00-foundations/01-internet-and-application-basics/21-proxmox-control-plane-storage-vm-networking/README.md)
* [Bridged networking and VM connectivity](../02-theory/00-foundations/01-internet-and-application-basics/22-bridged-networking-and-vm-connectivity/README.md)
* [SSH key-based authentication](../02-theory/00-foundations/01-internet-and-application-basics/23-ssh-key-based-authentication/README.md)

### Operating System Fundamentals

* [What is an operating system](../02-theory/00-foundations/02-operating-system-fundamentals/01-what-is-an-operating-system/README.md)
* [OS as abstraction layer between hardware and applications](../02-theory/00-foundations/02-operating-system-fundamentals/02-os-as-abstraction-layer-between-hardware-and-applications/README.md)
* [Tasks of an OS (CPU, memory, file, device, security, networking management)](../02-theory/00-foundations/02-operating-system-fundamentals/03-tasks-of-an-os/README.md)
* [Multi-user and multitasking systems](../02-theory/00-foundations/02-operating-system-fundamentals/04-multi-user-and-multitasking-systems/README.md)
* [Kernel vs user space](../02-theory/00-foundations/02-operating-system-fundamentals/05-kernel-vs-user-space/README.md)
* [System calls vs shell commands](../02-theory/00-foundations/02-operating-system-fundamentals/06-system-calls-vs-shell-commands/README.md)
* [Windows vs macOS vs Linux](../02-theory/00-foundations/02-operating-system-fundamentals/07-windows-vs-mac-os%20vs-linux/README.md)
* [Client OS vs server OS](../02-theory/00-foundations/02-operating-system-fundamentals/08-client-os-vs-server-os/README.md)
* [Why Linux is preferred in DevOps](../02-theory/00-foundations/02-operating-system-fundamentals/09-why-linux-is-preferred-in-devops/README.md)

---

## PHASE 1: LINUX & SYSTEM ENGINEERING (CORE BASE)

### Linux Architecture & Internals

* [Linux operating system overview](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/01-linux-operating-system-overview/README.md)
* [Linux architecture](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/02-linux-architecture/README.md)
* [Kernel responsibilities](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/03-kernel-responsibilities/README.md)
* [Linux boot process (BIOS/UEFI → GRUB → kernel → init/systemd)](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/04-linux-boot-process/README.md)
* [Filesystem hierarchy (FHS)](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/05-file-system-hierarchy/README.md)
* [File types](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/06-file-types/README.md)
* [Inodes](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/07-inodes/README.md)
* [Hard links vs soft links](../02-theory/01-linux-and-system-engineering/01-linux-architecture-and-internals/08-hard-links-vs-soft-links/README.md)

### File, User & Permission Management

* Navigation & directory listing
* File & directory management
* Viewing & paging files
* Search & text processing (grep, awk, sed)
* Permissions & ownership
* umask
* sudo
* User & group management
* /etc/passwd, /etc/shadow, UID/GID concepts

### Environment, Packages & Power

* Environment variables & shell behavior
* Bash fundamentals
* Package management (APT, YUM, DNF)
* Repositories & PPAs
* Binary vs source installs
* System shutdown & reboot
* Boot targets & rescue modes

### Processes, Services & Scheduling

* Process lifecycle (fork, exec, exit)
* Signals
* Job control
* systemd architecture
* Units, targets, dependencies
* Service lifecycle
* Service failures & restart policies
* Cron jobs & scheduling

### Logs, Storage & Memory

* System logs vs application logs
* journald / journalctl
* Log locations & rotation
* Disk partitions & filesystems
* Disk mounting
* Volumes
* LVM
* Swap
* Memory management basics

### Linux Networking & Security

* Networking fundamentals
* DNS resolution
* SSH, SCP, SFTP
* Firewall management (iptables, nftables, ufw)

### Common Linux Production Issues

* Service not starting
* Permission denied
* Disk full
* High CPU / memory usage
* Zombie processes
* Networking failures

---

## PHASE 2: VERSION CONTROL & ENGINEERING COLLABORATION

### Git Fundamentals & Advanced

* Version control concepts
* Git internals (objects, refs)
* Repository, commit, branch, HEAD
* Branching strategies (Git Flow, trunk-based)
* Merge vs rebase
* Conflict resolution
* Tags & releases
* Commit hygiene
* Conventional commit messages
* Undoing changes (restore, reset, revert, amend)
* Stash & pop
* Cherry-pick
* Squash merge
* Git hooks
* Interactive rebase

### Platforms & Collaboration

* GitHub
* GitHub workflows
* Pull requests & reviews
* PR lifecycle
* README engineering
* Markdown proficiency
* Engineering communication
* GitHub as public portfolio

---

## PHASE 3: NETWORKING, PORTS & LOAD BALANCING

### Core Networking

* OSI model
* TCP/IP layers
* Common protocols (TCP, UDP, ICMP)
* IP addressing
* Subnets & CIDR
* Routing fundamentals
* Ports & sockets
* TCP handshakes
* DNS fundamentals & outage impact

### Web & Security

* HTTP methods
* HTTP status codes
* HTTP vs HTTPS
* SSL/TLS handshake
* Certificates & CAs

### Load Balancing & Network Services

* L4 vs L7 load balancers
* Transport vs application layer behavior
* Reverse proxies
* Nginx fundamentals
* Nginx load balancing
* Load balancer algorithms
* NAT
* Security groups
* VPC peering
* Transit gateways
* VPN fundamentals

### Network Debugging

* ping
* netstat / ss
* nslookup / dig
* curl
* traceroute
* tcpdump basics

---

## PHASE 4: AUTOMATION & PROGRAMMING FOR DEVOPS

### Shell / Bash Scripting

* Shell execution model
* Variables & scope
* Conditionals
* Loops
* Positional parameters
* Pipes & redirects
* Exit codes
* Error handling
* Logging in scripts
* Defensive scripting
* Idempotency concepts
* Backup automation
* File & directory automation
* User & permission automation
* Cron-based automation
* Integration with AWS CLI
* Integration with APIs

### Python for DevOps

* Python syntax & control flow
* Functions & modules
* Virtual environments
* Exception handling
* File & JSON/YAML handling
* Logging
* API interaction
* Boto3 for AWS automation
* Infrastructure scripting mindset
* Flask basics (service awareness)

---

## PHASE 5: CONTAINERIZATION

### Docker Fundamentals

* Containers vs virtual machines
* Namespaces & cgroups (conceptual)
* Images vs containers
* Container lifecycle

### Docker Tooling & Image Design

* Docker CLI
* Dockerfile writing
* Multi-stage builds
* Image optimization
* Image hardening
* Layer caching
* Environment variables
* Entrypoint vs CMD
* Health checks

### Volumes, Networking & Compose

* Volumes vs bind mounts
* Container networking
* Docker Compose
* Service dependency ordering

### Operations & Troubleshooting

* Container logs & metrics
* Container registries
* Image scanning basics
* Containers exiting unexpectedly
* Port exposure issues
* Missing dependencies

---

## PHASE 6: CLOUD FUNDAMENTALS (VENDOR-AGNOSTIC + AWS)

### Cloud Basics

* Cloud computing models (IaaS, PaaS, SaaS)
* AWS / Azure / GCP overview
* Shared Responsibility Model

### IAM & Security

* IAM users, groups, roles
* Policies
* Access boundaries
* Least privilege

### Compute & Networking

* EC2 / VM concepts
* Instance lifecycle
* AMIs / images
* VPC
* CIDR blocks
* Public & private subnets
* Route tables
* Security groups
* NACLs

### Storage & Databases

* Object storage (S3)
* Block storage (EBS)
* File storage (EFS)
* RDS basics
* DynamoDB basics
* Database scaling strategies
* Backup & restore

### Advanced Cloud Concepts

* AWS CLI
* Autoscaling groups
* Load balancers
* Multi-AZ vs multi-region
* Disaster recovery patterns
* RPO & RTO
* Caching (Redis / ElastiCache)
* CDN fundamentals (CloudFront)

### Cost Awareness

* FinOps principles
* Cost allocation
* Resource cleanup
* Cost-conscious architecture

---

## PHASE 7: CI/CD & DELIVERY ENGINEERING

### CI/CD Foundations

* CI vs CD
* Pipeline as code
* Secure pipelines

### Jenkins

* Jenkins installation
* Controller vs agent model
* Declarative pipelines
* Scripted pipelines
* Shared libraries
* Plugins
* RBAC
* Notifications
* Pipeline failure handling
* Rollback concepts

### GitHub Actions

* Workflow syntax
* Runners
* Secrets
* Artifacts
* Environment-based deployments
* Workflow optimization

### Delivery Engineering

* Build stages
* Testing stages
* Security scanning
* Artifact repositories
* Deployment strategies (blue/green, canary)
* Rollbacks
* Failure handling
* Pipeline observability

### Tooling Evaluation

* Jenkins vs GitHub Actions vs GitLab CI
* Tool selection criteria
* MVP documentation

---

## PHASE 8: INFRASTRUCTURE AS CODE & CONFIGURATION MANAGEMENT

### Terraform (IaC)

* Infrastructure as Code concepts
* HCL syntax
* Terraform workflow
* Providers
* Variables & locals
* State management
* Remote backends
* Locking
* Provisioners & user data
* Workspaces
* Modules & reuse
* Scaling & destroy workflows
* Multi-cloud capability

### Ansible (Configuration Management)

* Ansible fundamentals
* Agentless architecture
* Terraform vs Ansible
* Inventory management
* Playbooks
* Roles
* Idempotency

---

## PHASE 9: KUBERNETES & PLATFORM ENGINEERING

### Kubernetes Core

* Why Kubernetes exists
* Kubernetes architecture
* Control plane components
* Worker nodes
* Local clusters (Kind, Minikube)

### Core Objects & YAML

* Namespaces
* Pods
* ReplicaSets
* Deployments
* StatefulSets
* Jobs & CronJobs
* Labels & selectors
* YAML structure

### Networking & Storage

* Services
* ClusterIP / NodePort / LoadBalancer
* Ingress controllers
* DNS in Kubernetes
* Storage fundamentals
* Persistent Volumes
* Persistent Volume Claims
* Stateful workloads

### Configuration & Security

* ConfigMaps
* Secrets
* Environment injection
* Resource requests & limits
* Readiness & liveness probes
* Pod security context
* RBAC

### Operations & Advanced Topics

* kubectl mastery
* Debugging pods
* Rolling updates
* Cluster upgrades
* Node maintenance
* GPU workloads
* EKS with Terraform

### Failure Scenarios

* CrashLoopBackOff
* ImagePullBackOff
* Misconfigured services
* Resource exhaustion
* Scaling failures

---

## PHASE 10: HELM & GITOPS

### Helm

* Helm architecture
* Charts
* Values
* Templating
* Upgrades
* Rollbacks

### GitOps

* GitOps principles
* Declarative deployments
* Git as source of truth
* GitOps vs traditional CI/CD
* Argo CD
* CI with GitHub Actions

---

## PHASE 11: OBSERVABILITY, SECURITY & RELIABILITY (SENIOR LEVEL)

### Observability & Monitoring

* Metrics, logs, traces
* Golden signals
* Prometheus
* Grafana
* Alerting best practices
* Dashboards
* SLOs & SLIs
* Logging pipelines (ELK)
* OpenTelemetry
* Debugging methodology

### Security & DevSecOps

* Image scanning
* Dependency scanning
* SonarQube
* Trivy
* OWASP Dependency-Check
* Secrets management
* AWS Secrets Manager
* Parameter Store
* Kubernetes RBAC hardening
* SBOM

### Reliability Engineering & SRE

* Reliability mindset
* Incident lifecycle
* On-call practices
* Alert fatigue
* Pager systems
* Runbooks
* Postmortems (blameless)
* Risk management
* Platform engineering concepts

---

## PHASE 12: PRODUCTION REALITY, JOB READINESS & FUTURE SYSTEMS

### Production Reality Engineering

* Greenfield vs brownfield systems
* Legacy systems
* Manual processes
* Change management
* Human error
* Risk-based decisions

### Documentation & Decision Making

* Architecture Decision Records (ADR)
* Design documents
* RFC-style proposals
* Runbooks vs playbooks
* Operational documentation

### Job & Interview Engineering

* Resume engineering (STAR)
* Business impact storytelling
* Downtime reduction narratives
* GitHub portfolio
* Projects > certificates
* Scenario-based interviews
* Debugging interviews
* DevOps system design interviews

### Agentic AI & AIOps

* AI agents
* Python-based agents
* Agent orchestration
* Log analysis agents
* Fix-suggestion agents
* Incident response automation
* AIOps on AWS
* MCP
* Copilot-style internal tools

---

## How to Use This Correctly

* Treat each phase as incomplete until something breaks
* README.md (clear, structured, professional)
* Write runbooks and postmortems, not just code
* Architecture diagram
* Failure scenarios & fixes
* Push everything to GitHub (even incident notes)
* Revisit older phases as your skill matures (senior engineers loop back)

---

## END GOAL

A senior DevOps / Cloud Architect who can:

* Design resilient systems
* Operate production platforms
* Debug failures under pressure
* Balance speed, cost, and reliability
* Mentor others
* Own systems end-to-end
