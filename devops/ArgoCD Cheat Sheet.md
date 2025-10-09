## 🚀 **ArgoCD Cheat Sheet**

---

### 🧠 **What is ArgoCD?**

- **ArgoCD (Argo Continuous Delivery)** is a **GitOps tool** for Kubernetes.
    
- It **automatically syncs** your Git repository (the desired state) with your Kubernetes cluster (the live state).
    
- It ensures **declarative, version-controlled deployments** — any config change in Git triggers a cluster update.
    

---

### ⚙️ **Core Concepts**

|Concept|Description|
|---|---|
|**Application**|Represents a deployed app in Kubernetes — linked to a Git repo and target cluster/namespace.|
|**Repository**|Git repo where your manifests or Helm charts are stored.|
|**Sync**|The process of applying Git changes to the cluster.|
|**Target Revision**|Git branch, tag, or commit that ArgoCD tracks.|
|**Sync Policy**|Determines how synchronization happens (manual or auto).|
|**Health Status**|Indicates if an app is healthy, degraded, or out of sync.|
|**Projects**|Logical grouping of applications with defined access controls.|

🏗️ **Architecture Overview**

```
           ┌────────────┐
           │  Developer │
           └─────┬──────┘
                 │ Push code
                 ▼
           ┌──────────────┐
           │ Git Repo      │
           │ (Manifests)   │
           └─────┬────────┘
                 │ Pull manifests
                 ▼
           ┌──────────────┐
           │ ArgoCD Server│
           │ (API + UI)   │
           └─────┬────────┘
                 │ Sync via K8s API
                 ▼
           ┌──────────────┐
           │ Kubernetes    │
           │ Cluster       │
           └──────────────┘

```

---

### 🔧 **Installation**
```
# Install ArgoCD (namespace: argocd)
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Get initial admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# Port forward to access UI
kubectl port-forward svc/argocd-server -n argocd 8080:443

```


💻 CLI Login
```
argocd login <ARGOCD_SERVER> --username admin --password <PASSWORD>
```


🧩 Creating Applications
Using CLI
```
argocd app create myapp \
  --repo https://github.com/example/repo.git \
  --path k8s \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```

Using YAML
```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: myapp
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/example/repo.git
    targetRevision: main
    path: k8s
  destination:
    server: https://kubernetes.default.svc
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

```
kubectl apply -f myapp.yaml
```


🔁 Common Commands
```
# List all applications
argocd app list

# Get app status
argocd app get myapp

# Sync an application (deploy changes)
argocd app sync myapp

# Refresh from Git
argocd app refresh myapp

# Rollback to previous version
argocd app rollback myapp --revision <commit-id>

# Delete application
argocd app delete myapp
```

---

### 🔐 **Sync Policies**

|Policy|Description|
|---|---|
|**Manual**|You trigger sync manually using CLI/UI.|
|**Automated**|ArgoCD automatically syncs whenever Git changes.|
|**Self-Heal**|Automatically corrects drift between Git and live cluster.|
|**Prune**|Deletes resources removed from Git.|

---

### 📊 **Health & Sync Status**

|Status|Meaning|
|---|---|
|**Synced**|Cluster matches Git.|
|**OutOfSync**|Cluster differs from Git.|
|**Healthy**|All components are running correctly.|
|**Degraded**|Some components failed or unhealthy.|

---

### 🧱 **Integration Examples**

- **GitHub Actions / Jenkins** → triggers Git push → ArgoCD auto-syncs → K8s updated.
    
- **Helm Support:** ArgoCD supports Helm charts directly.
    
- **Kustomize Support:** Works with overlays for environments (dev/stage/prod).
    

---

### 🧰 **Best Practices**

- Organize Git repos with **one folder per environment**.
    
- Enable **Auto Sync + Self Heal** for production apps.
    
- Use **RBAC and Projects** to isolate team access.
    
- Integrate **SSO (OIDC, SAML)** for authentication.
    
- Implement **ApplicationSet** for managing multi-cluster or multi-env deployments.
    
- Always store manifests in **Git**, not the cluster.
    
- Use **Argo Rollouts** for canary and blue/green deployments.
    

---

### 🧭 **Troubleshooting**

```
# Check logs
kubectl logs -n argocd deploy/argocd-server
kubectl logs -n argocd deploy/argocd-repo-server

# Check app events
kubectl get events -n argocd
argocd app history <app-name>
```


---

### 🧠 **ArgoCD vs Jenkins vs FluxCD**

|Feature|ArgoCD|Jenkins|FluxCD|
|---|---|---|---|
|Deployment Type|GitOps (pull)|CI/CD (push)|GitOps (pull)|
|UI Dashboard|✅|❌|❌|
|Auto-Sync|✅|❌|✅|
|Drift Detection|✅|❌|✅|
|Helm/Kustomize Support|✅|Partial|✅|

