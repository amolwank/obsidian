Kubernetes is an open-source container orchestration platform.
In simple terms its a manager for your containers. 

###### **Key Features:**
- Automated Scheduling:
- Self-Healing:
- [[Scaling]]: ([[HPA]])
- Service Discovery and Load Balancing:
- Storage Management:
- Rolling Updates and Rollbacks:

###### [[Kubernetes Architecture]]:
Kubernetes follows a master-worker (control plane & node) architecture
###### Basic Kubernetes Objects
- [[Pod]] -> Smallest deployable unit (containers).
- [[Deployment]] -> Manages Pods (scaling, updates)
- [[Service]] -> Exposes Pods (ClusterIP, NodePort, LoadBalancer).
- [[ConfigMap]]/[[Secret]] -> Store configs and secrets.
- [[Namespace]] -> Logical cluster separation.
- [[Ingress]] -> Expose HTTP(S) traffic to servers.
- [[PersistentVolume (PV)]] / PersistentVolumeClaim (PVC) -> Storage
- [[ReplicaSet]] -> Ensures a specific number of pod replicas.
- [[StatefulSet]] -> Manages a stateful applications (stable networks IDs,persistent storage).
- [[DaemonSet]] -> Ensures one Pod per node (like logging agents) 
- [[Job]] -> Run tasks to completion.
- [[CronJobs]] -> Runs jobs on a schedule. 
[[LivenessProbe and ReadinessProbe]]

[[Kubernetes Add-ons]]


1. [[Core Workload Resource]]
2. [[Service and Networking Resources]]
3. [[Configuration & Secrets]]
4. [[Storage Resources]]
5. [[Cluster-Level Resources]]
[[Deployment Strategies]] 
[[Service Accounts]]
[[RBAC]]
[[IRSA]]
[[Metric Server]]


Tags: #Kubernetes
#flashcards 

---

# 🔥 Top 15 Kubernetes & EKS Interview Questions (Senior Level)

### **1. What’s the difference between Deployment, ReplicaSet, and StatefulSet?** 
-[[Difference between Deployment, ReplicaSet and StatefulSet]]
- **Deployment**: Manages stateless apps, scaling & rolling updates.
- **ReplicaSet**: Ensures a fixed number of Pod replicas (usually managed by Deployment).
- **StatefulSet**: For stateful apps, preserves Pod identity (name, storage, ordering).

---

### **2. How does Kubernetes handle service discovery?**
-[[Service Discovery]]
- Each Pod gets an IP, but not stable.
- **Services (ClusterIP, NodePort, LoadBalancer)** expose stable endpoints.
- Uses **kube-dns/CoreDNS** for service name resolution.

---

### **3. How do you debug a pod stuck in `CrashLoopBackOff`?**

- Check logs: `kubectl logs <pod>`
    
- Check events: `kubectl describe pod <pod>`
    
- Common causes: bad image, misconfigured env vars, liveness/readiness probe failures.
    

---

### **4. What is [[RBAC]] in Kubernetes?**

- **Role-Based Access Control** → controls who can do what in the cluster.
    
- Roles/ClusterRoles + RoleBindings/ClusterRoleBindings.
    
- Used to enforce **least-privilege access**.
    

---

### **5. [[ConfigMap vs Secret – difference]]?**

- **ConfigMap**: Stores non-sensitive config (URLs, flags).
    
- **Secret**: Stores sensitive data (passwords, tokens, certs).
    
- Secrets are base64-encoded, can integrate with external secret managers.
    

---

### **6. What’s the difference between HPA, VPA, and Cluster Autoscaler?** - [[Scaling]]

- **HPA**: Scales Pods based on CPU/memory/custom metrics.
    
- **VPA**: Adjusts Pod resource requests/limits.
    
- **Cluster Autoscaler**: Adds/removes worker nodes.
    

---

### **7. How do you [[Provision an EKS cluster with Terraform]]?**

- Use `terraform-aws-eks` module.
- Create VPC + Subnets → EKS cluster → Node groups.
- Attach IAM roles/policies for nodes & IRSA for Pods.
    

---

### **8. What’s the difference between managed node groups, self-managed nodes, and Fargate in EKS?**

- **Self-managed**: Full control, you manage lifecycle.
- **Managed node groups**: AWS automates patching & upgrades.
- **Fargate**: Serverless Pods, no node management.

---

### **9. What is IRSA (IAM Roles for Service Accounts)?**
- Maps a **Kubernetes Service Account** to an **IAM Role**.
- Allows Pods to access AWS resources securely without storing keys.
- Requires EKS OIDC provider.
---

### **10. What is the VPC CNI plugin in EKS?** - [[VPC CNI Plugin]]
- AWS CNI allows Pods to get IPs directly from VPC subnets.
- Pros: Better integration with AWS networking.
- Cons: IP exhaustion risk if many Pods.
---
### **11. How do you configure Ingress in EKS?**
- Install **Ingress Controller** (ALB Ingress Controller, NGINX).
- Create `Ingress` resource mapping host/path → Services.
- ALB Ingress integrates with AWS ALB for external traffic.
---
### **12. How do you secure communication between Pods?** - [[Secure Communication bet Pods]]
- Use **Network Policies** for L3/L4 rules.
- For service-to-service security → mTLS via **Istio/Linkerd**.
- Enforce Pod Security Standards (restricted privilege).

---

### **13. How do you handle secrets in Kubernetes securely?**

- Store in **Secrets** (mounted as env vars or volumes).
    
- Use **KMS integration** (AWS Secrets Manager, HashiCorp Vault).
    
- Enable **encryption at rest** in etcd.
    

---

### **14. How do you monitor EKS clusters?**

- **CloudWatch Container Insights** for logs/metrics.
    
- **Prometheus + Grafana** for custom metrics/dashboards.
    
- **FluentBit/Fluentd + OpenSearch/Elasticsearch** for log aggregation.
    

---

### **15. How do you optimize EKS cost?**

- Use **Cluster Autoscaler + Spot Instances** with On-Demand fallback.
    
- Use **Fargate for burst workloads**.
    
- Right-size Pods with HPA/VPA.
    
- Scale down non-prod clusters after office hours.
    

---

✅ **Memory Tip**: Break into 3 groups:

- **K8s Core** (Deployment, RBAC, Autoscaling, ConfigMap vs Secret, Pod debugging)
    
- **EKS Specific** (IRSA, OIDC, VPC CNI, Node groups, Ingress, Monitoring)
    
- **Best Practices** (Security, Cost Optimization, Scaling)
    

---
## 🔹 Kubernetes – Senior-Level Interview Questions

### **Architecture & Core Concepts**

- Can you explain the Kubernetes control plane components (API server, etcd, scheduler, controller manager)?- [[Kubernetes control plane components]]
- How do Pods, ReplicaSets, and Deployments differ?
- When would you use a StatefulSet vs a Deployment?
- How does Kubernetes handle service discovery and load balancing internally?
### **Networking & Security**
- Explain the Kubernetes networking model (Pod-to-Pod, Pod-to-Service).
- What are Network Policies? How do you enforce isolation between namespaces?
- How do you secure communication between Pods (mTLS, Istio)?
- What is RBAC in Kubernetes and how do you design least-privilege access?
### **Config & Secrets Management**

- Difference between ConfigMap and Secret? When to use which?
- How would you integrate external secret managers (like AWS Secrets Manager or HashiCorp Vault)?
    

### **Scaling & Reliability**

- How does Horizontal Pod Autoscaler (HPA) work?
- Difference between HPA, VPA (Vertical Pod Autoscaler), and Cluster Autoscaler?
- How do you design a multi-region highly available Kubernetes cluster?- [[Design a multi-region highly available Kubernetes Cluster]]

### **Operations & Monitoring**

- How do you debug a pod stuck in `CrashLoopBackOff` or `Pending`?
- How do you monitor Kubernetes (tools like Prometheus, Grafana, Datadog)?
- How do you handle node failures in Kubernetes?
### **Storage & Data**
- Explain Persistent Volume (PV) vs Persistent Volume Claim (PVC).
- How do you handle storage in stateful workloads on Kubernetes?    
- What’s the difference between CSI (Container Storage Interface) drivers and in-tree storage?

### **CI/CD & GitOps**

- How do you deploy applications to Kubernetes using GitHub Actions/Jenkins/ArgoCD?
- What’s the difference between Helm and Kustomize? Which one have you used?
- How do you implement Canary or Blue/Green deployments in Kubernetes?

---

## 🔹 AWS EKS – Senior-Level Interview Questions

### **Cluster Design & Provisioning**

- How do you provision an EKS cluster using Terraform/IaC?
- What’s the difference between self-managed nodes, managed node groups, and Fargate profiles in EKS?
- How would you design multi-account/multi-region EKS clusters for DR?- [[Multi-account Multi-region EKS Cluster for DR]]

### **Security & Identity**
- What is IAM Roles for Service Accounts (IRSA) in EKS? Why is it important?
- How do you integrate OIDC identity provider with EKS?  
- How do you enforce Pod Security Standards (PSS) in EKS?

### **Networking in EKS**
- How does the VPC CNI plugin work in EKS?
- What’s the difference between ClusterIP, NodePort, and LoadBalancer services in EKS?
- How do you configure an ALB Ingress Controller vs NGINX Ingress Controller in EKS?
### **Scaling & Cost Optimization**
- How do you configure Cluster Autoscaler with EKS?
- How do you run spot instances in EKS while ensuring high availability?
- How would you optimize EKS cluster cost for dev vs prod environments?

### **Observability & Troubleshooting**

- How do you integrate CloudWatch, Prometheus, and Grafana with EKS?- [[Integrate Cloudwatch, Prometheus and Grafana]]
- How would you troubleshoot pods not being scheduled in EKS?
- What’s the process if EKS API server becomes unavailable?
    

---

