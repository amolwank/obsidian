## Types of Autoscaling in Kubernetes

### 1. **Horizontal Pod Autoscaler (HPA)**

- Scales the **number of pod replicas** in a Deployment/ReplicaSet based on **CPU, memory, or custom metrics**.
- Example: If CPU usage > 80%, HPA adds more pods.
```
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 80
```
### 2. **Vertical Pod Autoscaler (VPA)**

- Adjusts the **CPU and memory requests/limits** of containers in pods.
- Useful when workloads change resource requirements but pod count doesn’t need to change.
- Typically used for batch jobs or workloads where scaling pods isn’t efficient.
---

### 3. **Cluster Autoscaler (CA)**

- Scales the **number of worker nodes** in a cluster.
- Works with cloud providers (AWS, GCP, Azure).
- If HPA requests more pods but no resources are available → Cluster Autoscaler provisions a new node.
    

---
## 🔹 How They Work Together

- **HPA** ensures pod count matches workload demand.
- **VPA** ensures pods have the right resource allocation.
- **Cluster Autoscaler** ensures enough nodes are available to host pods.

---
## 🔹 Interview-Ready Answer (Short)

“Kubernetes supports autoscaling at three levels: HPA scales pods horizontally, VPA adjusts CPU/memory resources vertically, and Cluster Autoscaler adds/removes nodes based on demand. Together, they provide efficient resource utilization and handle varying workloads automatically.”

### ⏱️ **60-sec Answer (Crisp)**

- **HPA (Horizontal Pod Autoscaler):** Scales **pods** up/down based on CPU/memory/custom metrics.
    
- **VPA (Vertical Pod Autoscaler):** Adjusts **CPU/memory requests & limits** of a pod dynamically.
    
- **Cluster Autoscaler:** Scales the **nodes** in the cluster (adds/removes worker nodes) based on pending pods or underutilization.
    

👉 In short: **HPA → pods count, VPA → pod size, Cluster Autoscaler → node count.**

---

### ⏱️ **2–3 min Answer (Detailed)**

In Kubernetes:

- **HPA (Horizontal Pod Autoscaler):**
    
    - Automatically changes the **number of replicas** in a Deployment/ReplicaSet/StatefulSet.
        
    - Works by watching metrics (CPU%, memory, or custom metrics from Prometheus/CloudWatch).
        
    - Example: If CPU > 70% for all pods, HPA increases replicas.
        
- **VPA (Vertical Pod Autoscaler):**
    
    - Adjusts the **resources assigned** to a pod (CPU/memory requests & limits).
        
    - Useful for apps that cannot scale horizontally (like stateful apps, databases).
        
    - Example: If pod consistently OOMs, VPA increases memory request.
        
- **Cluster Autoscaler (CA):**
    
    - Works at the **infrastructure level** (node scaling).
        
    - If pods are pending due to lack of resources, CA provisions new nodes.
        
    - If nodes are underutilized and pods can be rescheduled, CA removes nodes.
        
    - On AWS EKS, this integrates with Auto Scaling Groups.
        

🔑 **Key difference:**

- HPA → workload-level scaling (pods count).
    
- VPA → resource-level scaling (CPU/memory per pod).
    
- Cluster Autoscaler → infra-level scaling (nodes).
    

---

⚡Memory Trick:  
Think **“Pods–Pods–Nodes”**

- HPA → more Pods,
    
- VPA → bigger Pods,
    
- Cluster Autoscaler → more Nodes.
    

---