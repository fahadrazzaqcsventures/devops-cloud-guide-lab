# Incident Response – Network Lockout

## Incident Summary

The Proxmox host became unreachable over the network due to a misconfiguration in virtual bridge or firewall settings. SSH access from the management network was lost, resulting in a full management-plane lockout.

This incident simulates a common real-world failure where administrative access is accidentally blocked on a production virtualization host.

---

## Detection

**Symptoms observed:**

* Proxmox Web UI inaccessible via browser
* SSH connection attempts timing out
* No response to ICMP (ping) from management workstation

**Initial hypothesis:**

* Network bridge misconfiguration (vmbr0)
* Firewall rule blocking management traffic

---

## Impact Assessment

* **Control Plane:** Unavailable
* **Data Plane:** VMs continued running without interruption
* **Severity:** High (management outage)
* **Blast Radius:** Single host

---

## Response Timeline

### Step 1: Access Host via Physical / Console Access

* Accessed Proxmox host directly via:

  * Local console (keyboard + monitor) OR
  * Proxmox physical terminal

**Rationale:** Network-based recovery impossible without management access.

---

### Step 2: Verify Network Interface Status

```bash
ip addr
ip link
```

* Identified active physical NIC
* Verified interface state (UP/DOWN)

---

### Step 3: Inspect Bridge Configuration

```bash
cat /etc/network/interfaces
```

* Confirmed vmbr0 configuration
* Detected misconfiguration:

  * Incorrect bridge port
  * Missing gateway OR
  * Incorrect IP assignment

---

### Step 4: Temporarily Restore Minimal Connectivity

Edited network configuration to a known-good minimal setup:

```bash
auto vmbr0
iface vmbr0 inet static
    address <correct-ip>
    netmask <correct-netmask>
    gateway <correct-gateway>
    bridge_ports <physical-nic>
    bridge_stp off
    bridge_fd 0
```

**Principle:** Restore access first, optimize later.

---

### Step 5: Restart Networking Safely

```bash
ifreload -a
# or as fallback
systemctl restart networking
```

* Avoided full reboot
* Monitored console for errors

---

### Step 6: Validate Connectivity

```bash
ip route
ping <gateway>
ping 8.8.8.8
```

* Network connectivity restored
* Verified outbound routing

---

### Step 7: Restore Remote Management Access

* SSH access verified
* Proxmox Web UI accessible again

---

## Root Cause Analysis

**Primary Cause:**

* Misconfiguration of Proxmox network bridge during manual changes

**Contributing Factors:**

* No prior validation of changes
* No out-of-band management interface

---

## Lessons Learned

* Network changes on hypervisors are high-risk
* Console access is mandatory for recovery
* Control plane failures can be self-inflicted

---

## Follow-Up Actions

* Document known-good network configuration
* Create a rollback-safe change procedure
* Add network change checklist to runbooks

---

## Status

* Incident resolved
* No data loss
* No VM downtime
