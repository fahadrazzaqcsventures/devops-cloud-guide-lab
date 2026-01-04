# How the Internet Works

This document covers the **foundational theory** required for DevOps, Cloud, and Platform Engineering. You must understand this before touching infrastructure. Every outage, latency issue, DNS failure, or security incident ultimately traces back to these concepts.

---

## 1. What Is the Internet?

The internet is a **global, decentralized network of networks**. It connects independent networks (ISPs, data centers, cloud providers, enterprises) using standardized protocols so that data can be exchanged reliably.

Key properties:

* Decentralized (no single owner)
* Packet-switched (data broken into packets)
* Fault-tolerant by design
* Built on open standards (TCP/IP)

In DevOps terms:

> The internet is the **transport layer for applications**, APIs, CI/CD systems, monitoring, and cloud services.

---

## 2. Clients, Servers, and Requests

### Client

A client is any system that **initiates a request**.
Examples:

* Browser
* Mobile app
* CLI tools (curl, kubectl, terraform)

### Server

A server is any system that **responds to requests**.
Examples:

* Web servers (Nginx, Apache)
* API servers
* Databases

DevOps relevance:

* Servers fail
* Clients retry
* Load balancers sit between them

---

## 3. IP Addresses and Ports

### IP Address

An IP address uniquely identifies a machine on a network.

Types:

* IPv4 (e.g., 192.168.1.10)
* IPv6 (cloud-native future)

### Ports

Ports identify **which application** on a machine should receive traffic.

Examples:

* 80 → HTTP
* 443 → HTTPS
* 22 → SSH

DevOps failures:

* Wrong port exposed
* Firewall blocking ports
* Port conflicts

---

## 4. DNS (Domain Name System)

DNS translates **human-readable names** into IP addresses.

Example flow:

```
www.example.com → DNS → 93.184.216.34
```

Why DNS matters:

* Most outages are *not* application failures — they are DNS failures
* CI/CD, Kubernetes, cloud services all depend on DNS

DevOps mindset:

> If DNS is broken, everything is broken.

---

## 5. TCP/IP Model (Practical View)

| Layer       | Responsibility   | DevOps Impact     |
| ----------- | ---------------- | ----------------- |
| Application | HTTP, HTTPS, SSH | App configs, APIs |
| Transport   | TCP/UDP          | Retries, timeouts |
| Network     | IP routing       | Subnets, VPCs     |
| Link        | Ethernet/WiFi    | Bridges, NICs     |

You troubleshoot **top-down or bottom-up** depending on symptoms.

---

## 6. How a Web Request Works (End-to-End)

Example: Opening a website

1. Browser checks local cache
2. DNS resolves domain to IP
3. TCP connection established (3-way handshake)
4. TLS handshake (HTTPS)
5. HTTP request sent
6. Server processes request
7. Response returned
8. Browser renders content

DevOps failures can happen at **any step**.

---

## 7. Stateless vs Stateful Communication

### Stateless

* Each request independent
* Easier to scale
* Used by modern cloud apps

### Stateful

* Server remembers client state
* Harder to scale
* Common in legacy systems

Why DevOps prefers stateless:

* Enables autoscaling
* Simplifies failure recovery

---

## 8. Latency, Bandwidth, and Reliability

* **Latency**: Time delay
* **Bandwidth**: Data volume per second
* **Reliability**: Consistency of delivery

DevOps optimization focuses on:

* Reducing latency (CDNs, caching)
* Improving reliability (retries, HA)

---

## 9. Internet Failures You Must Expect

Common real-world failures:

* DNS outage
* Packet loss
* Network partition
* ISP routing issues
* TLS certificate expiry

Senior DevOps principle:

> Assume the network will fail. Design accordingly.

---

## 10. DevOps Takeaways

* The internet is unreliable by default
* Applications must tolerate failure
* Observability starts at the network layer
* Most production issues are networking-related

This knowledge directly feeds into:

* Load balancing
* Kubernetes networking
* Cloud VPC design
* Incident response

---

## Next Step

Proceed to:
[**Theory → What Is a Server**](../02-what-is-a-server/README.md)
