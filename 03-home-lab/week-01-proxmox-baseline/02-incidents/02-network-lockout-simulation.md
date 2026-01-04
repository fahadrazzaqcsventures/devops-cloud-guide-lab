# Week 1 – Failure 2: Network Lockout Simulation

This failure simulates one of the **most common and dangerous production incidents**: losing network access to a critical host.

Senior engineers are judged heavily on how they **prevent, detect, and recover** from lockouts.

---

## 1. Objective

By completing this failure, you will learn to:

* Understand Proxmox / Linux networking at a practical level
* Recover access using out-of-band methods
* Avoid panic-driven mistakes
* Build disciplined recovery documentation

---

## 2. Pre-Failure Safety Check (Mandatory)

Before breaking anything, confirm:

* Physical console access is working
* You can log in locally as root or sudo user
* You understand current network configuration

Commands to run **before breaking**:

```
ip addr
ip route
brctl show
```

Save this output for documentation.

---

## 3. Failure Injection Methods (Choose ONE)

### Option A – Bridge Misconfiguration (Recommended)

Action:

```
# Bring down the main bridge
ip link set vmbr0 down
```

Result:

* SSH disconnects
* Web UI unreachable
* Host still running

---

### Option B – Firewall Lockout

Action:

```
ufw deny ssh
ufw enable
```

Result:

* SSH blocked
* Console still available

---

## 4. Expected Symptoms

* SSH session drops
* Web UI inaccessible
* Ping to host fails
* VMs may lose connectivity

This is what real outages feel like.

---

## 5. Recovery Procedure (Console Only)

### Step 1: Access Console

* Use physical keyboard + monitor
* Log in locally

---

### Step 2: Diagnose

```
ip addr
ip link
ip route
```

Identify missing or down interfaces.

---

### Step 3: Restore Network

If bridge down:

```
ip link set vmbr0 up
```

If firewall issue:

```
ufw disable
```

---

### Step 4: Verify

```
ip addr
ping -c 3 <gateway>
```

Confirm SSH and UI access restored.

---

## 6. Lessons to Internalize

* Never experiment without console access
* Bridges are critical failure points
* Networking failures feel worse than they are
* Calm diagnosis beats fast guessing

---

## 7. Mandatory Documentation Outputs

You must now create:

* Incident (network lockout)
* Incident Response
* Decision log
* Runbook: Host network lockout
* ADR (only if design decision changes)

Follow the same rigor as Failure 1.

---

## 8. Senior Engineer Check

You are successful only if:

* You did not reboot blindly
* You restored access via diagnosis
* You documented before moving on

---

## Documentation Links

* [**Incident Report**](../docs/01-incident-reports/network-lockout.md) — what broke
* [**Incident Response**](../docs/02-incident-responses/promox-network-lockout.md) — how it was fixed
* [**Decision**](../docs/03-decisions.md/network-lockout.md) — why specific actions were chosen
* [**Runbook**](../docs/04-runbooks/promox-network-lockout-recovery.md)— how to recover next time without thinking
* [**ADR**](../docs/05-adrs/promox-network-change-safety.md) — architecture changes
