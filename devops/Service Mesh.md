## 🔹 **What is a Service Mesh?**
A **Service Mesh** is a dedicated infrastructure layer for **managing service-to-service communication** within a microservices architecture.

In Kubernetes, it is typically implemented using a **sidecar proxy** (like Envoy) that runs alongside each pod.

---
## 🔹 **Why We Need It?**
Kubernetes handles **service discovery and load balancing**, but it does not provide:

- **mTLS encryption between pods**
- **Traffic routing (blue/green, canary)**
- **Retry, failover, and circuit breaking**
- **Detailed observability (metrics, tracing, logging)**
👉 A service mesh fills this gap.
---
## 🔹 **How It Works in Kubernetes**
1. Each pod has a **sidecar proxy** injected (usually via an Admission Controller).
2. All traffic **in and out of the pod** goes through this proxy.
3. The mesh’s **control plane** manages policies, certificates, and routing rules.
4. The **data plane** (proxies) enforces those rules in real time.
    

**Popular Service Meshes**:
- **Istio** (most popular, uses Envoy)
- **Linkerd** (lightweight, simpler)
- **Consul**
---
## 🔹 **Use Cases in Kubernetes**
1. **Security**    
    - Enforces **mTLS** (mutual TLS) for pod-to-pod encryption.
    - Provides authentication & authorization.
2. **Traffic Management**
    - Canary or blue/green deployments.
    - Request routing (e.g., send 10% of traffic to v2).
    - Automatic retries and failover.
3. **Observability**
    - Collects detailed telemetry: metrics, logs, traces.
    - Provides service-level insights without modifying app code.
---
## ✅ **Interview One-liner**

“A Service Mesh in Kubernetes is a dedicated layer that manages service-to-service communication using sidecar proxies. It provides **mTLS security, traffic control, and observability** without requiring changes in application code.”

---