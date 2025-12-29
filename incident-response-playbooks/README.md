# Incident Response Playbooks

This document provides **step-by-step incident response playbooks** for all major failure types in your unified home lab plan. Each playbook is designed to:

* Teach troubleshooting methodology
* Encourage root-cause analysis
* Produce portfolio-ready documentation

Each incident is structured as:

1. **Scenario**
2. **Detection**
3. **Immediate Actions**
4. **Root Cause Analysis**
5. **Recovery Steps**
6. **Postmortem Documentation**

---

## 1. Linux VM Service Failure

**Scenario:** Nginx or systemd service fails to start

**Detection:**

* `systemctl status nginx` shows inactive or failed
* Logs: `/var/log/nginx/error.log`, `journalctl -xe`

**Immediate Actions:**

1. Check unit file: `systemctl cat nginx`
2. Restart service: `sudo systemctl restart nginx`
3. Check for port conflicts: `sudo netstat -tulnp | grep :80`

**Root Cause Analysis:**

* Incorrect permissions on `/etc/nginx/sites-enabled`
* Missing dependencies
* Port already in use

**Recovery Steps:**

1. Correct permissions: `sudo chmod 644 /etc/nginx/sites-enabled/*`
2. Kill conflicting process: `sudo kill <pid>`
3. Restart service and validate `curl http://localhost`

**Postmortem Documentation:**

* Record commands used, root cause, and lessons learned
* Include before/after config snapshots

---

## 2. SSH Lockout

**Scenario:** Cannot SSH into VM

**Detection:**

* Timeout or `Permission denied` messages

**Immediate Actions:**

1. Use Proxmox console access
2. Check `/etc/ssh/sshd_config` and authorized_keys

**Root Cause Analysis:**

* Wrong permissions on `.ssh` directory or `authorized_keys`
* SSH service misconfigured

**Recovery Steps:**

1. Correct `.ssh` permissions: `chmod 700 ~/.ssh` and `chmod 600 ~/.ssh/authorized_keys`
2. Restart SSH: `sudo systemctl restart ssh`

**Postmortem Documentation:**

* Note mistake and future prevention
* Update runbook with corrected commands

---

## 3. Disk Full / Storage Issue

**Scenario:** Disk reaches 100%

**Detection:**

* `df -h` shows 100% usage
* Services failing with `No space left on device`

**Immediate Actions:**

1. Identify large files: `sudo du -sh /* | sort -h`
2. Clean logs or temp files

**Root Cause Analysis:**

* Log rotation not configured
* Backup scripts misconfigured

**Recovery Steps:**

1. Delete unnecessary files
2. Implement log rotation: `logrotate`
3. Reboot services if necessary

**Postmortem Documentation:**

* Document storage issue and log rotation config
* Update automation scripts to prevent recurrence

---

## 4. Container Crash / Port Collision

**Scenario:** Docker container exits unexpectedly

**Detection:**

* `docker ps` shows container stopped
* Logs: `docker logs <container>`

**Immediate Actions:**

1. Inspect logs
2. Check ports: `docker ps -a | grep <port>`
3. Start container with verbose flags

**Root Cause Analysis:**

* Missing environment variables
* Port conflict
* Volume mount errors

**Recovery Steps:**

1. Correct env vars or Dockerfile
2. Free conflicting ports
3. Recreate container

**Postmortem Documentation:**

* Record fix, configuration changes, lessons learned

---

## 5. Kubernetes Pod Crash / NotReady Node

**Scenario:** Pod in CrashLoopBackOff or Node NotReady

**Detection:**

* `kubectl get pods` shows CrashLoopBackOff
* `kubectl get nodes` shows NotReady

**Immediate Actions:**

1. Describe pod: `kubectl describe pod <pod>`
2. Check logs: `kubectl logs <pod>`
3. Node health: `kubectl get events`

**Root Cause Analysis:**

* Misconfigured deployment, insufficient resources
* Node reboot or network misconfiguration

**Recovery Steps:**

1. Correct deployment YAML
2. Drain and uncordon node: `kubectl drain <node>` then `kubectl uncordon <node>`
3. Restart pods or redeploy

**Postmortem Documentation:**

* Capture YAML before/after
* Document resource allocation decisions
* Note lessons for future scaling

---

## 6. DNS Resolution Failure

**Scenario:** DNS server (Pi-hole/CoreDNS) not responding

**Detection:**

* `nslookup google.com` fails

**Immediate Actions:**

1. Restart DNS service
2. Check Pi firewall rules

**Root Cause Analysis:**

* Service crashed
* Wrong network configuration

**Recovery Steps:**

1. Validate `/etc/resolv.conf`
2. Restart service: `sudo systemctl restart pihole-FTL`

**Postmortem Documentation:**

* Document configuration change
* Update network diagram

---

## 7. CI/CD Pipeline Failure

**Scenario:** Pipeline fails to build or deploy

**Detection:**

* Jenkins or GitHub Actions shows failed stage

**Immediate Actions:**

1. Inspect build logs
2. Check credentials, secrets
3. Validate environment variables

**Root Cause Analysis:**

* Missing dependencies
* Invalid secret
* Network issue for deployment target

**Recovery Steps:**

1. Fix environment or secret
2. Re-run pipeline
3. Validate deployed artifact

**Postmortem Documentation:**

* Pipeline YAML before/after
* Lessons for secret management

---

## 8. Multi-Service Outage / DR Simulation

**Scenario:** Multiple components fail simultaneously

**Detection:**

* Monitoring alerts
* Pod failures, service unavailability

**Immediate Actions:**

1. Prioritize services (SLOs)
2. Restart critical services first

**Root Cause Analysis:**

* Correlated misconfigurations
* Network partition or node outage

**Recovery Steps:**

1. Sequential recovery using runbooks
2. Validate each service before next
3. Record all actions in incident log

**Postmortem Documentation:**

* Blameless postmortem
* Update architecture diagram
* Plan future mitigation

---

## Usage Notes

* **Every incident is a training exercise**
* Always document each step
* Use failures as GitHub portfolio entries
* Run playbooks in sequence to simulate real-world escalation

This document ensures you **practice SRE, DevOps, and platform engineering simultaneously** while maintaining a strong portfolio.
