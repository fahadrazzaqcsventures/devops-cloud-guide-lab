# ADR: SSH Access Hardening on Proxmox

## ADR ID

ADR-PLX-SEC-001

## Status

Accepted

## Date

Week 1 – Foundations

---

## Context

The Proxmox host represents the **primary management and control plane** for all virtualized workloads in the home lab. Default SSH configurations allow password-based authentication, which increases the attack surface and operational risk.

At the same time, Proxmox requires **root SSH access** for legitimate platform operations such as cluster communication, migrations, backups, and console access across nodes. A naïve hardening approach (e.g., disabling root login entirely) would break platform functionality.

---

## Decision

Implement **SSH key-only authentication** on the Proxmox host with the following constraints:

* Disable all password-based SSH authentication
* Allow `root` login **only via SSH keys**
* Use configuration snippets under `/etc/ssh/sshd_config.d/` to remain upgrade-safe
* Validate configuration syntax before reload to prevent lockout

Specifically:

* `PasswordAuthentication no`
* `PermitRootLogin prohibit-password`
* `PubkeyAuthentication yes`
* Disable keyboard-interactive authentication

---

## Rationale

* SSH keys provide stronger cryptographic guarantees than passwords
* Eliminating passwords removes common brute-force and credential-stuffing vectors
* `prohibit-password` preserves required Proxmox root workflows
* Snippet-based configuration avoids conflicts during package upgrades
* Explicit validation (`sshd -t`) reduces human error risk

This approach balances **security hardening** with **platform operability**.

---

## Consequences

### Positive

* Reduced attack surface on the management plane
* Clear and auditable access mechanism
* Consistent with industry best practices
* Zero impact on Proxmox core functionality

### Negative

* Loss of password-based emergency access (mitigated by console access)
* Requires proper SSH key management discipline

---

## Alternatives Considered

1. **Disable root SSH login entirely**

   * Rejected: breaks Proxmox workflows and cluster features

2. **Allow both password and key authentication**

   * Rejected: weakens security posture unnecessarily

3. **Restrict SSH to non-root users only**

   * Rejected: increases operational complexity without meaningful security gain

---

## Compliance and Scope

This ADR applies to:

* All Proxmox hosts in the home lab
* Any future Proxmox nodes added

---

## Review Conditions

Revisit this decision if:

* Proxmox introduces alternative secure control-plane access methods
* Hardware-based access controls (e.g., IPMI, out-of-band management) are added
* Multi-user admin access model is required

---

**Decision Type:** Security / Access Control
**Phase:** Week 1 – Foundations
