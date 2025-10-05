### **ReplicaSet**

- Ensures a specified number of **Pod replicas** are running.
- If a Pod crashes, ReplicaSet replaces it.
- Usually not used directly — managed by Deployments.

---
### **Deployment**

- A higher-level abstraction over ReplicaSets.
- Manages stateless applications.
- Provides features like **rolling updates, rollbacks, scaling, and history tracking**.
- Example: Web servers, APIs.

---
### **StatefulSet**

- Manages **stateful applications** where Pod identity matters.
- Provides:    
    - Stable network IDs (Pod names)
    - Persistent storage (via PVCs).
    - Ordered, graceful deployment & scaling.
- Example: Databases (MySQL, Cassandra, Kafka).
    
---

## 🎯 **Quick Interview Answer (30 sec)**

> “ReplicaSet ensures the desired number of Pods run, but it’s usually controlled by a Deployment, which adds rollout, rollback, and scaling features for stateless apps. For stateful apps that need persistent identity and storage, we use StatefulSets, which guarantee stable Pod names, ordered scaling, and persistent volumes.”