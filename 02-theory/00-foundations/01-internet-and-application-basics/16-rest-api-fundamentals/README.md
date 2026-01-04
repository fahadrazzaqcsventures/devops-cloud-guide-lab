# REST API Fundamentals

This document explains the fundamentals of **REST (Representational State Transfer) APIs**, which are the backbone of modern web services and microservices architectures.

Understanding REST is critical for DevOps engineers because APIs are central to service communication, CI/CD automation, monitoring, and incident response.

---

## 1. Why This Topic Matters

* Most backend services expose functionality via REST APIs
* CI/CD pipelines often interact with APIs for deployment, health checks, and automation
* Understanding REST helps debug failures and design reliable systems

---

## 2. Core Principles of REST

1. **Client-Server Architecture**

   * Separation of concerns: client handles UI, server handles business logic and data

2. **Statelessness**

   * Each request from the client must contain all information needed to process it
   * No session state stored on the server

3. **Cacheable**

   * Responses should indicate whether they are cacheable to improve performance

4. **Uniform Interface**

   * Standard HTTP methods (GET, POST, PUT, DELETE) for actions
   * Resource-based URLs (e.g., `/users`, `/orders/{id}`)

5. **Layered System**

   * Client may not know whether it is connected to end server or intermediary

6. **Code on Demand (optional)**

   * Servers can send executable code to clients (rare in practice)

---

## 3. HTTP Methods

| Method | Purpose                      |
| ------ | ---------------------------- |
| GET    | Retrieve resource            |
| POST   | Create resource              |
| PUT    | Update resource (idempotent) |
| PATCH  | Partial update               |
| DELETE | Remove resource              |

---

## 4. Response Codes

* **2xx** Success
* **4xx** Client error (bad request, unauthorized)
* **5xx** Server error (internal error, service unavailable)

---

## 5. Home Lab Mapping

* Build a simple REST API using Flask or Node.js
* Implement endpoints for CRUD operations connected to your database
* Test using `curl` or Postman
* Simulate failures:

  * Return 500 errors on DB outage
  * Incorrect response format to test client handling

---

## 6. You Should Now Clearly Understand

* REST APIs define a **standardized communication method** between services
* HTTP methods and response codes are crucial for automation and debugging
* Properly designed APIs simplify CI/CD pipelines, monitoring, and scaling
* Your home lab will allow hands-on practice of API design, testing, and failure simulations

---

## Next Theory Topic

[**What is DevOps (culture, feedback loops, ownership)**](../17-what-is-devops/README.md)