# 🚀 Kubernetes Senior-Level Interview Cheat Sheet

---

## 1. **Core Concepts**

- **Cluster Components**
    
    - **Control Plane:**
        
        - **API Server** → entry point, validates requests.
            
        - **etcd** → key-value store, cluster state.
            
        - **Controller Manager** → watches & reconciles desired vs actual state.
            
        - **Scheduler** → assigns Pods to Nodes.
            
    - **Worker Node:**
        
        - **kubelet** → agent running pods.
            
        - **kube-proxy** → networking, service load balancing.
            
        - **Container Runtime** → Docker, containerd, CRI-O.
            

**Q:** Difference between kubelet & kube-proxy?  
👉 Kubelet ensures pods run, kube-proxy handles networking.

---

## 2. **Workload Resources**

- **Pod** → Smallest deployable unit.
    
- **ReplicaSet** → Ensures desired # of pods.
    
- **Deployment** → Declarative updates (rolling, blue/green).
    
- **StatefulSet** → Pods with stable identity & storage (DBs).
    
- **DaemonSet** → Runs pod on every node (logging, monitoring agents).
    
- **Job / CronJob** → Batch/cron tasks.
    

---

## 3. **Services & Networking**

- **ClusterIP** → Internal-only access.
    
- **NodePort** → Expose service on node’s IP:Port.
    
- **LoadBalancer** → External access via cloud LB.
    
- **Ingress** → HTTP/HTTPS routing with host/path rules.
    
- **CNI Plugins** → Calico, Flannel, Cilium for networking.
    

---

## 4. **Storage**

- **PersistentVolume (PV)** → Storage resource in cluster.
    
- **PersistentVolumeClaim (PVC)** → Request storage from PV.
    
- **StorageClass** → Dynamic provisioning (EBS, Ceph, NFS).
    
- **ConfigMap & Secret** → Config mgmt, credentials.
    

---

## 5. **Scaling**

- **Horizontal Pod Autoscaler (HPA)** → Scale pods based on CPU/memory/custom metrics.
    
- **Vertical Pod Autoscaler (VPA)** → Adjust pod resources automatically.
    
- **Cluster Autoscaler** → Scale worker nodes up/down.
    

---

## 6. **Security**

- **RBAC (Role-Based Access Control)** → Grant minimal privileges.
    
- **Service Accounts** → Identities for pods.
    
- **Network Policies** → Restrict pod-to-pod traffic.
    
- **Secrets** → Store credentials (better: use KMS/SSM).
    
- **Pod Security Standards** → Enforce policies (privileged, baseline, restricted).
    

**Q:** How do you secure inter-pod communication?  
👉 Use Network Policies + TLS + mTLS with service mesh (Istio/Linkerd).

---

## 7. **Observability**

- **Logs** → `kubectl logs`.
    
- **Monitoring** → Prometheus + Grafana.
    
- **Tracing** → Jaeger, OpenTelemetry.
    
- **Alerting** → Alertmanager.
    
- **kubectl top** → Check resource usage.
    

---

## 8. **CI/CD & GitOps**

- **Helm** → Package manager (charts).
    
- **Kustomize** → YAML customization.
    
- **ArgoCD / Flux** → GitOps deployment.
    
- **Jenkins X / Tekton** → CI/CD pipelines.
    

---

## 9. **High Availability & DR**

- Run **multi-master control plane**.
    
- Use **etcd backup/restore**.
    
- Deploy across **multiple AZs/regions**.
    
- Use **PodDisruptionBudgets (PDBs)** & **Anti-affinity rules**.
    

---

## 10. **Advanced Topics**

- **Operators** → Custom controllers (CRDs).
    
- **Sidecar Pattern** → Logging, proxy, security agents.
    
- **Service Mesh** → Istio, Linkerd for traffic management, mTLS, observability.
    
- **Pod Priority & Preemption** → Ensure critical pods get scheduled.
    
- **Resource Quotas & Limits** → Prevent noisy neighbors.
    

---

## 11. **Important Commands**