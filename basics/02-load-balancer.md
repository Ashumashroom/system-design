# Load Balancing & Consistent Hashing in System Design

---

## 📌 What is Load Balancing?

Load balancing is the process of **distributing incoming traffic** across **multiple backend servers** to ensure that no single server gets overwhelmed.

> It improves **scalability**, **availability**, and **reliability** of systems.

---

## 🚦 Why Load Balancing?

- Prevents server overload
- Increases fault tolerance
- Reduces latency
- Enables horizontal scaling
- Handles high concurrency

---

## ⚙️ How Load Balancing Works

A Load Balancer acts as an intermediary between users and servers.


---

## 🧠 Load Balancing Algorithms

### 1. Round Robin
- Sends requests to servers in circular order.

### 2. Least Connections
- Sends to the server with the fewest active connections.

### 3. IP Hash
- Maps client IP to specific server (useful for sticky sessions).

### 4. Weighted Round Robin
- Distributes more requests to powerful servers.

---

## 🌐 Types of Load Balancers

| Type            | Description                         | Examples                    |
|------------------|-------------------------------------|-----------------------------|
| Hardware         | Physical load balancer appliance    | F5 Networks                 |
| Software         | Application-based balancer          | Nginx, HAProxy              |
| Cloud-based      | Managed by cloud provider           | AWS ELB, GCP LB, Azure LB   |
| DNS-based        | Load balancing via DNS responses    | AWS Route 53, Cloudflare    |

---

## 🔑 Key Concepts

- **Health Checks**: Detect if servers are healthy.
- **Failover**: Reroute if one server fails.
- **Sticky Sessions**: Maintain session on the same server.
- **SSL Termination**: Offload HTTPS decryption to the load balancer.

---

## 🧩 Use Cases

- Web applications
- Video streaming platforms
- Microservices architecture
- API Gateways

---

## 📷 Visual Overview

![Load Balancing](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Load_balancing.svg/1200px-Load_balancing.svg.png)

---

# 🌀 Consistent Hashing (System Design Notes)

---

## 📌 What is Consistent Hashing?

Consistent Hashing is a technique used in distributed systems to **distribute keys/data** across servers **efficiently**, even when the number of servers changes dynamically.

> It minimizes the number of keys that need to be remapped when a server is added or removed.

---

## ❌ Problem with Normal Hashing

In normal hashing, keys are mapped using:
```plaintext
hash(key) % N   → N = number of servers
```

### 🔴 Issue:
- If `N` changes (e.g., new server added), **most keys get reassigned**.
- This causes:
  - Massive data movement
  - Cache misses
  - Poor scalability and performance

### 📉 Example:
- Original setup: `hash("video1") % 3 = Server 0`
- Add server: `hash("video1") % 4 = Server 2`
- Now, almost **all keys are reassigned**

---

## ✅ Why Use Consistent Hashing?

### 🧠 Key Idea:
- Treat the hash space as a **circle (ring)** from 0 to 2³².
- Hash both **keys** and **servers** onto this ring.
- Each key is assigned to the **first server clockwise** from its hash.

```
       [Server A]
          ↑     \
[Key1]         [Server C]
   ↑             ↑
[Key2]         [Server B]
```

### 🔁 When a Server is Added:
- Only a **small portion of keys** are moved to the new server.
- Most keys continue being served by the same server.

---

## 🧱 Architecture Summary

### 🔄 Hash Ring
- Servers and keys mapped to a circular hash space (0 to 2³²)
- Key goes to first server clockwise from its hash

### ⚖️ Example Flow:
1. Hash "user123" → position = 65
2. Circle has servers at positions: S1 (20), S2 (50), S3 (90)
3. "user123" is assigned to S3

---

## 🔧 Enhancements

### 🔹 Virtual Nodes
- Each server is mapped to **multiple points** on the ring
- Helps balance uneven key distribution

### 🔹 Replication
- A key is stored on **multiple clockwise nodes**
- Increases **fault tolerance**

---

## 📊 Consistent Hashing vs Normal Hashing

| Feature                  | Normal Hashing (`% N`)        | Consistent Hashing                  |
|--------------------------|-------------------------------|-------------------------------------|
| Key remapping on scaling | High (most keys change)       | Low (few keys move)                 |
| Cache performance        | Poor                          | Stable                              |
| Scalability              | Difficult                     | Easy to add/remove servers          |
| Data movement            | Heavy                         | Minimal                             |
| Used in                  | Legacy systems (rarely now)   | Redis, Cassandra, DynamoDB, CDNs    |

---

## ✅ Summary

- Normal hashing fails at scale due to massive remapping
- Consistent hashing solves this by organizing servers/keys on a ring
- Only affected keys move on server join/leave
- Critical for **scalable, cache-friendly, fault-tolerant** systems
