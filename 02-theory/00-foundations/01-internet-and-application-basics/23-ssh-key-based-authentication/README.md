# SSH Key-Based Authentication

This document explains **how SSH key-based authentication works under the hood**, why it is mandatory for modern infrastructure, and how it fits into Proxmox, Linux servers, and cloud environments.

This is not about memorizing commands. This is **access-control and trust engineering**.

---

## 1. Why This Matters

Password-based SSH access fails in production for predictable reasons:

* Brute-force attacks
* Credential reuse
* Phishing and leaks
* Shared admin passwords
* Lack of non-repudiation

Senior engineers do not ask:

> “What is the root password?”

They ask:

> “Which key authenticated this session, and who owns it?”

SSH keys are the **foundation of secure automation, cluster communication, and cloud access**.

---

## 2. Authentication vs Authorization

Before understanding SSH keys, separate these concepts:

* **Authentication** → Who are you?
* **Authorization** → What are you allowed to do?

SSH keys solve **authentication**. RBAC, sudo, and policies handle authorization.

---

## 3. How SSH Authentication Works

### Password-Based Flow (Legacy)

1. Client sends username
2. Server requests password
3. Password is transmitted (encrypted, but still reusable)
4. Server validates against stored secret

**Problems:**

* Secret can be guessed
* Secret can be reused
* Secret can be stolen

---

### Key-Based Flow (Modern)

SSH uses **public-key cryptography**.

1. Client proves possession of a **private key**
2. Server verifies using the **public key**
3. No secret is transmitted

> The private key never leaves the client machine.

---

## 4. Key Pair Model

Each SSH identity consists of:

* **Private key** → kept secret on your laptop
* **Public key** → stored on servers

The server does **not** know your private key.
It only knows which public keys are trusted.

This reverses the traditional password trust model.

---

## 5. SSH Trust Boundary

Trust is established when:

* A public key is added to `~/.ssh/authorized_keys`
* The SSH daemon accepts that key for a user

Removing access is trivial:

* Delete one line from `authorized_keys`

No password rotation required.

---

## 6. Why SSH Keys Are Mandatory in Proxmox

Proxmox relies on SSH for:

* Cluster communication
* VM migrations
* Replication
* Automation (Ansible, scripts)
* Emergency recovery

Password-based root access:

* Breaks automation
* Encourages shared credentials
* Increases blast radius

**Key-based root access is the Proxmox-safe model.**

---

## 7. Root Login: The Subtle but Critical Detail

Incorrect hardening causes lockouts.

### Dangerous Setting

```
PermitRootLogin no
```

This blocks **all** root access — including keys.

### Correct Production Setting

```
PermitRootLogin prohibit-password
```

* Root login allowed
* Password authentication blocked
* Key-based access preserved

This is the industry-standard compromise.

---

## 8. SSH Daemon Responsibility

`sshd` enforces:

* Authentication methods
* Allowed users
* Allowed keys
* Cryptographic algorithms

Misconfiguring `sshd` is a **control-plane outage**.

Always validate before reload:

```
sshd -t
```

---

## 9. SSH Keys and Automation

Every modern DevOps tool assumes SSH keys:

* Git
* Ansible
* Terraform (remote provisioners)
* CI/CD runners
* Kubernetes node access

Passwords do not scale.
Keys do.

---

## 10. Mapping to Cloud Concepts

| Proxmox / Linux | Cloud Equivalent  |
| --------------- | ----------------- |
| SSH key         | EC2 key pair      |
| authorized_keys | Instance metadata |
| Root login      | Cloud admin user  |

Cloud platforms **disable password SSH by default** for a reason.

---

## 11. Common Failure Scenarios

* Lost private key
* Wrong file permissions on `~/.ssh`
* Disabled root login incorrectly
* SSH reload without validation

**Lesson:**

> SSH hardening mistakes cause instant self-inflicted outages.

---

## 12. You Should Now Clearly Understand

* Why passwords are insecure at scale
* How SSH key authentication actually works
* Why Proxmox depends on SSH trust
* How root access must be hardened safely
* Why this is a foundation topic, not an advanced one

---

## Next Theory Topic

[**What is an operating system**](../../02-operating-system-fundamentals/01-what-is-an-operating-system/README.md)

---

## Next Step

You are now ready to build [**Week 1 hands-on labs**](../../../../03-home-lab/01-promox/week-01-proxmox-baseline/README.md):

* Proxmox baseline configuration
* Network bridges
* SSH access
* First VM creation

This is where theory turns into muscle memory.
