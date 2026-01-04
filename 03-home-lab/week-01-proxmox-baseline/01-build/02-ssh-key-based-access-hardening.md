# Build Phase 2 – SSH Key-Based Access Hardening

## Objective

Eliminate password-based administrative access to the Proxmox host and enforce **SSH key-based authentication** while preserving Proxmox operational requirements.

This step hardens the **management plane** without breaking cluster-safe root access.

---

## Purpose

* Remove password-based attack surface
* Enforce cryptographic authentication
* Align with production security baselines
* Prevent accidental lockout of Proxmox services

---

## Preconditions

* Proxmox host is fully updated and rebooted (Build Phase 1 completed)
* Stable SSH access using password authentication
* Console access available as a safety fallback

---

## Actions

### 1. Generate SSH Key on Personal Laptop

```bash
ssh-keygen -t ed25519 -C "proxmox-root-access" -f ~/.ssh/proxmox_root
```

**Why:**

* Uses modern, secure elliptic-curve cryptography
* Creates a dedicated keypair for Proxmox root access

---

### 2. Copy Public Key to Proxmox Host

```bash
ssh-copy-id -i /home/fahad/.ssh/proxmox_root.pub root@192.168.111.111
```

**Why:**

* Installs key into `authorized_keys`
* Preserves correct permissions automatically

---

### 3. Verify Key-Based SSH Login

```bash
ssh root@192.168.111.111
```

**Validation:**

* Login succeeds without password prompt
* Session is stable

⚠️ **Do NOT continue until this succeeds**

---

### 4. Disable Password-Based SSH Authentication

Create a hardened SSH configuration snippet:

```bash
nano /etc/ssh/sshd_config.d/99-disable-password.conf
```

Paste the following:

```bash
# Disable all password-based authentication (keys only)
PasswordAuthentication no

# Allow root login only with keys (Proxmox-safe)
PermitRootLogin prohibit-password

# Explicitly enable key authentication
PubkeyAuthentication yes

# Disable keyboard-interactive authentication
KbdInteractiveAuthentication no
ChallengeResponseAuthentication no
```

**Critical Note:**

❌ Do NOT set:

```text
PermitRootLogin no
```

This would block key-based root login and break Proxmox operations.

---

### 5. Validate SSH Configuration (MANDATORY)

```bash
sshd -t
```

**Expected:**

* No output
* No errors

This step prevents accidental lockout.

---

### 6. Reload SSH Service Safely

```bash
systemctl reload ssh
```

**Why:**

* Applies new configuration
* Does NOT terminate existing sessions

---

## Validation Checklist

* [x] SSH login works using key only
* [x] Password login is rejected
* [x] Root login works via key
* [x] Existing sessions remain active

---

## Expected Outcome

* Password-based SSH access disabled
* Root access secured via SSH keys
* Proxmox functionality preserved

---

## Failure Awareness

Potential failure scenarios:

* SSH config syntax error
* Key not properly installed
* Accidental root lockout

**Recovery:**

* Use console access
* Revert SSH config snippet
* Reload SSH service

---

## Documentation

* Record key usage policy
* Reference this step in security ADRs
* Tag this as a **security hardening baseline**

---

## Engineering Principle Reinforced

> Secure access before scaling responsibility.

Authentication is a control-plane concern, not an afterthought.
