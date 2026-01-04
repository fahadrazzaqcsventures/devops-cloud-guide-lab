# Week 1 – Failure 1: Control Plane Disruption

This failure simulates a **control plane outage** where management access is lost, but workloads continue running. This is a critical concept for DevOps and platform engineers to internalize early.

---

## 1. Objective

By completing this failure, you will learn to:

* Distinguish between control plane and data plane responsibilities
* Understand why management outages do not always equal service outages
* Avoid unnecessary reboots or destructive actions
* Document incidents with production-grade clarity

---

## 2. Pre-Failure Safety Check (Mandatory)

Before injecting the failure, confirm:

* You have console or SSH access to the Proxmox host
* No critical configuration changes are in progress
* You understand which service provides the Proxmox Web UI

Useful validation command:

```
systemctl status pveproxy
```

---

## 3. Failure Injection Method

### Control Plane Service Stop

**Action:**

```
# Stop the Proxmox web (control plane) service
sudo systemctl stop pveproxy

# Verify service state
sudo systemctl status pveproxy
```

This intentionally disrupts the management interface only.

---

## 4. Expected Symptoms

After stopping the service, you should observe:

* Proxmox Web UI becomes unreachable
* SSH access remains available
* Running VMs continue operating normally
* No data loss or VM crashes

This mirrors real-world control plane disruptions.

---

## 5. Recovery Procedure

### Step 1: Verify VM State

Ensure workloads are still running:

```
qm list
```

---

### Step 2: Restore Control Plane

```
# Start the web service again
sudo systemctl start pveproxy
```

---

### Step 3: Verify Recovery

* Access the Proxmox Web UI
* Confirm service is active:

```
systemctl status pveproxy
```

---

## 6. Lessons to Internalize

* Control plane outages do **not** automatically mean workload outages
* Restarting services is often safer than rebooting hosts
* Panic-driven actions (reboot, reinstall) cause more harm than good
* Clear mental models prevent unnecessary downtime

> **Key lesson:** Control plane ≠ data plane

---

## 7. Mandatory Documentation Outputs

You must now create the following documents:

* Incident – what broke
* Incident Response – how it was handled
* Decision – tactical choices made
* Runbook – how to resolve this in the future
* ADR – only if architecture or design changes

---

## 8. Senior Engineer Check

You are successful only if:

* You did not reboot the host
* You verified VM continuity before fixing the UI
* You restored service cleanly
* You documented the incident before moving on

---

## Documentation Links

* [**Incident Report**](../docs/01-incident-reports/proxmox-control-plane-disruption.md) — what broke
* [**Incident Response**](../docs/02-incident-responses/proxmox-control-plane-disruption.md) — how it was fixed
* [**Decision**](../docs/03-decisions/proxmox-control-plane-handling.md) — why specific actions were chosen
* [**Runbook**](../docs/04-runbooks/proxmox-control-plane-outage.md) — future recovery steps
* [**ADR**](../docs/05-adrs/promox-control-plane-separation.md) — architectural impact (if any)
