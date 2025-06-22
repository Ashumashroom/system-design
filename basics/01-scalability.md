# Scalability in System Design

## What is Scalability?

Scalability is the system's ability to handle **increased load** (more users, requests, data) by **adding resources**, without sacrificing performance.

It answers the question:
> "Can this system grow efficiently as demand increases?"

---

## Types of Scalability

### 1. Vertical Scaling (Scaling Up)
- Add more power to existing machines (CPU, RAM, SSD).
- Easier to implement.
- Limited by hardware.

### 2. Horizontal Scaling (Scaling Out)
- Add more machines/nodes to distribute the load.
- More complex but better for large systems.
- Needs load balancing, distributed architecture.

---
### 📷 Visual Comparison:

![Horizontal vs Vertical Scaling](https://www.cloudzero.com/wp-content/uploads/2024/01/scaling-type.webp)


## Key Scalability Concepts

- **Load Balancing**
  - Distributes traffic among multiple servers.
  - Prevents any one server from being overwhelmed.

- **Caching**
  - Reduces repeated computations or DB queries.
  - Speeds up response time under load.

- **Sharding**
  - Split data across different databases (horizontal partitioning).

- **Stateless Services**
  - Makes it easier to add/remove servers since no session state is stored on server.

- **Auto-Scaling**
  - Automatically adds/removes instances based on usage metrics (e.g., CPU load).

---

## Scalability Metrics

- **QPS (Queries Per Second)**: Measures traffic load.
- **Latency**: Time taken to respond (should remain stable with scale).
- **Throughput**: Number of requests handled per unit time.
- **Resource Utilization**: CPU, memory, disk usage under load.

---

## Examples

- Scaling a Chat App:
  - Vertical: Increase DB server RAM to hold more messages in memory.
  - Horizontal: Add more chat servers and use a load balancer.

- Scaling a Video Streaming Service:
  - Use CDN for static content.
  - Shard metadata DB by user ID.

---

## Best Practices

- Design stateless microservices
- Use message queues for async processing
- Pre-calculate or cache expensive operations
- Monitor and auto-scale critical components

---

## Conclusion

Scalability is fundamental to building robust, high-traffic systems. The right scaling strategy depends on the system's nature, growth expectations, and cost tolerance.
