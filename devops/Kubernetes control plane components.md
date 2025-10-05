# 🔹 Kubernetes Control Plane Components

The **control plane** manages the cluster’s state and makes decisions.

### 1. **API Server (kube-apiserver)**
- The **front door of Kubernetes** – all communication goes through it.
- Exposes the Kubernetes API (REST + gRPC).
- Validates requests, enforces authentication/authorization, and updates `etcd`.
- Example: `kubectl get pods` → hits API server → gets data from etcd.
---
### 2. **etcd**
- **Key-value database** that stores the **entire cluster state**.
- Stores: pods, secrets, configmaps, deployments, events, etc.
- Highly available + consistent (uses Raft consensus).
- API server is the only component that talks directly to etcd.
---
### 3. **Scheduler (kube-scheduler)**
- Decides **which node runs a pod**.
- Watches for **unscheduled pods** in API server.
- Chooses a node based on:
    - Resource availability (CPU, memory)
    - Affinity/anti-affinity rules - [[Affinity and anti-affinity]]
    - [[Taints & tolerations]]
    - [[Topology spread (zones, racks)]]
- Example: If Pod A requests 2 CPUs → scheduler finds the best node → binds it.

---

### 4. **Controller Manager (kube-controller-manager)**
- Runs **controllers**, which are loops that watch cluster state and try to move it to the **desired state**.
- Types of controllers:
    - **Node controller** → checks node health.   
    - **Replication controller** → ensures desired number of pods.    
    - **Endpoint controller** → updates services/endpoints.    
    - **Job controller** → ensures jobs complete.    
- Example: If Deployment says 3 replicas but only 2 pods are running → controller creates the missing one.
---
# 🔑 **Analogy (Easy to Remember)**

- **API Server** → Reception desk (all requests come here).
- **etcd** → Filing cabinet (stores records/state).
- **Scheduler** → HR manager (decides who works where).
- **Controller Manager** → Operations manager (keeps things running as planned).
---
# ⚡ Interview One-liner

> “The API Server is the entry point, etcd is the state database, the Scheduler assigns pods to nodes, and the Controller Manager runs background controllers to reconcile desired vs actual state.”