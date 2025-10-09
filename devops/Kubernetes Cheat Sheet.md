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
    
- **[[CNI Plugins]]** → Calico, Flannel, Cilium for networking.
    

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
    
- **[[Network Policies]]** → Restrict pod-to-pod traffic.
    
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

---

## 🧩 **KUBERNETES CHEAT SHEET**

---

### 🚀 **Core Concepts**

| Component         | Description                                                             |
| ----------------- | ----------------------------------------------------------------------- |
| **Pod**           | Smallest deployable unit — runs one or more containers.                 |
| **ReplicaSet**    | Ensures desired number of identical Pods are running.                   |
| **Deployment**    | Manages stateless apps — updates, scaling, rollback.                    |
| **StatefulSet**   | Manages stateful apps — stable identity, ordered deployment.            |
| **DaemonSet**     | Runs one pod per node (for logging/monitoring agents).                  |
| **Job / CronJob** | Runs tasks to completion or on a schedule.                              |
| **Service**       | Exposes Pods via stable IP and DNS (ClusterIP, NodePort, LoadBalancer). |
| **Ingress**       | Manages external HTTP/S access to services.                             |
| **ConfigMap**     | Stores non-sensitive configuration data.                                |
| **Secret**        | Stores sensitive data like passwords or API keys.                       |
| **Namespace**     | Logical isolation for resources within a cluster.                       |
### ⚙️ **Common Commands**

#### **Basic Cluster Info**
```
kubectl version
kubectl cluster-info
kubectl get nodes
kubectl describe node <node-name>
```
Pods
```
kubectl get pods -A               # All namespaces
kubectl get pods -n <namespace>
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/bash

```
Deployments
```
kubectl get deploy
kubectl describe deploy <name>
kubectl rollout status deploy/<name>
kubectl rollout undo deploy/<name>
kubectl scale deploy <name> --replicas=3

```
Services
```
kubectl get svc
kubectl describe svc <svc-name>
kubectl expose deploy <deploy-name> --port=80 --target-port=8080 --type=LoadBalancer
```
Ingress
```
kubectl get ingress
kubectl describe ingress <name>
```
Namespaces
```
kubectl get ns
kubectl create ns dev
kubectl delete ns dev

```

ConfigMaps & Secrets
```
kubectl create configmap app-config --from-literal=ENV=prod
kubectl get configmap app-config -o yaml

kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=pass123
kubectl get secret db-secret -o yaml

```
---

### 🧱 **Storage & Volumes**

|Type|Description|
|---|---|
|**emptyDir**|Temporary storage, deleted when Pod restarts.|
|**hostPath**|Mounts a directory from host node.|
|**PersistentVolume (PV)**|Represents physical storage in the cluster.|
|**PersistentVolumeClaim (PVC)**|Request for PV by a user.|
|**StorageClass**|Defines dynamic provisioning of storage.|

```
kubectl get pv
kubectl get pvc
```
---

### 🔄 **Networking**

|Type|Description|
|---|---|
|**ClusterIP**|Internal access only (default).|
|**NodePort**|Exposes service on a static port on each node.|
|**LoadBalancer**|Integrates with cloud provider LB (AWS ELB, etc.).|
|**Ingress**|Path/host-based routing via HTTP/HTTPS.|

```
kubectl create serviceaccount my-sa
kubectl get serviceaccounts
kubectl describe sa my-sa
kubectl get roles,rolebindings,clusterroles,clusterrolebindings
```

- **RBAC:** Role-Based Access Control (Roles, RoleBindings)
    
- **NetworkPolicy:** Restrict Pod communication
    
- **Secrets:** Encrypted credentials
    

---

### 🧩 **Monitoring & Debugging**
```
kubectl get events
kubectl top pods
kubectl top nodes
kubectl describe pod <pod>
kubectl logs -f <pod> --previous
	
```
---

### 🧠 **Probes & Autoscaling**

| Type                | Purpose                                     |
| ------------------- | ------------------------------------------- |
| **Liveness Probe**  | Checks if app is alive, restarts if failed. |
| **Readiness Probe** | Checks if app is ready to receive traffic.  |
| **Startup Probe**   | Delays liveness checks during startup.      |

```
kubectl autoscale deploy <name> --min=2 --max=5 --cpu-percent=80
```
---

### 🛠️ **YAML Manifest Reference**

#### **Deployment Example**
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

Service Example
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
```
---

### 🧰 **Useful Shortcuts**

```
kubectl get all
kubectl get po,svc,deploy -A
kubectl delete pod --all
kubectl apply -f <file>.yaml
kubectl delete -f <file>.yaml
```

### 🧭 **Best Practices**

- Use **namespaces** for environment separation (dev, stage, prod).
    
- Use **labels & selectors** for grouping.
    
- Use **readiness/liveness probes** for health.
    
- Use **ConfigMaps & Secrets** for configuration.
    
- Implement **RBAC** for security.
    
- Use **Resource Limits/Requests** for CPU and memory.
    
- Use **Helm or Kustomize** for managing manifests.