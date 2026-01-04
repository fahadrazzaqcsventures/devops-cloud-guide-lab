# Client–Server Architecture

This document explains **Client–Server Architecture**, the fundamental interaction model behind the internet, enterprise systems, cloud platforms, and DevOps workflows. Every DevOps failure scenario ultimately involves a broken client–server interaction.

---

## 1. Definition

**Client–Server Architecture** is a model where:

* A **client** initiates a request
* A **server** processes the request and returns a response

They communicate over a network using agreed-upon protocols.

DevOps framing:

> A production system is a graph of clients and servers, not a single application.

---

## 2. Clients Explained

A client is anything that **consumes a service**.

Examples:

* Browser requesting a webpage
* CI pipeline calling an API
* Kubernetes kubelet calling the API server
* Terraform calling cloud APIs

Clients are:

* Stateless by design
* Retry-oriented
* Failure-sensitive

---

## 3. Servers Explained

A server is anything that **provides a service**.

Examples:

* Web server
* Application server
* Database server
* DNS server

Servers:

* Must handle concurrent clients
* Must enforce security
* Must degrade gracefully under load

---

## 4. Request–Response Lifecycle

Typical flow:

1. Client resolves server address (DNS)
2. Client opens network connection
3. Client sends request
4. Server validates request
5. Server processes business logic
6. Server sends response
7. Connection closes or is reused

Failure at any step causes user-visible impact.

---

## 5. State Management

### Stateless Client–Server

* No session stored on server
* Easy to scale horizontally
* Preferred in cloud-native systems

### Stateful Client–Server

* Server stores session state
* Requires stickiness or shared storage
* Harder to scale

DevOps rule:

> Stateless systems scale; stateful systems constrain.

---

## 6. Synchronous vs Asynchronous Communication

### Synchronous

* Client waits for response
* Simpler logic
* Sensitive to latency

### Asynchronous

* Client sends request and continues
* Uses queues or events
* More resilient

Cloud-native systems heavily favor asynchronous patterns.

---

## 7. One-Tier, Two-Tier, and Three-Tier Models

### One-Tier

* Client and server on same machine
* Not scalable

### Two-Tier

* Client ↔ Server
* Common in small systems

### Three-Tier

* Client ↔ Web ↔ Application ↔ Database
* Standard enterprise architecture

DevOps engineers usually operate **three-tier or more complex systems**.

---

## 8. Scaling Implications

Scaling happens on the **server side**:

* Horizontal scaling (add servers)
* Vertical scaling (add resources)

Clients must tolerate:

* Slow responses
* Retries
* Partial failures

---

## 9. Failure Scenarios (Real World)

Common client–server failures:

* DNS resolution failure
* Network timeout
* Server overload (5xx errors)
* Client retry storms
* Partial outages

Senior insight:

> Most outages are **interaction failures**, not code bugs.

---

## 10. Mapping to Your Home Lab

In your lab:

* Browser / curl → Client
* Nginx → Server
* Flask API → Server
* Kubernetes API → Server
* CI/CD pipelines → Clients

You will intentionally break client–server interactions to practice recovery.

---

## 11. DevOps Takeaways

* Everything is client–server
* Failures propagate across boundaries
* Observability must exist on both sides
* Design for retries and degradation

---

## You should be able to clearly explain:

* Why most outages are interaction failures, not code bugs
* How stateless client–server systems scale
* Why retries can cause outages if misdesigned
* How client–server boundaries multiply failure points

---

## Next Theory Topic

Proceed to:
[**Stateless vs Stateful Systems**](../06-stateless-vs-stateful-systems/README.md)
