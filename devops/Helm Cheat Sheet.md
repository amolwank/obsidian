---

## ⚙️ **HELM CHEAT SHEET**

---

### 🧠 **What is Helm?**

- **Helm** is the **package manager for Kubernetes** — like `apt` for Ubuntu or `yum` for RHEL.
    
- It helps you **package, configure, and deploy** Kubernetes applications using reusable templates called **charts**.
    
- Simplifies deployment of complex apps like **Prometheus, Nginx, MySQL, Jenkins**, etc.
    

---

### 🧩 **Core Concepts**

|Term|Description|
|---|---|
|**Chart**|A Helm package — contains all Kubernetes manifests (YAMLs).|
|**Release**|A deployed instance of a Helm chart in a cluster.|
|**Repository**|A collection of Helm charts (e.g., Bitnami, ArtifactHub).|
|**Values.yaml**|File containing customizable configuration values for a chart.|
|**Template**|YAML files with Go templating syntax (`{{ }}`) to create dynamic manifests.|

---

### 🏗️ **Helm Architecture**


```
     ┌────────────┐
     │  Chart Repo│
     └─────┬──────┘
           │
           ▼
     ┌────────────┐
     │  Helm CLI  │
     └─────┬──────┘
           │
           ▼
     ┌────────────┐
     │ Kubernetes │
     │   Cluster  │
     └────────────┘

```
Helm CLI interacts with the cluster using **Kubernetes API Server**.

---

### 💻 **Basic Commands**

#### 📦 **Chart Repositories**

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo list
helm repo update
helm search repo nginx
```

🚀 **Install / Upgrade / Rollback**

```
# Install chart
helm install my-nginx bitnami/nginx

# Install with custom values
helm install my-nginx bitnami/nginx -f values.yaml

# Upgrade release
helm upgrade my-nginx bitnami/nginx -f new-values.yaml

# Rollback to previous version
helm rollback my-nginx 1
```

🧹 **Uninstall / Delete**

```
helm uninstall my-nginx
```

🔍 **List / Inspect**

```
helm list
helm status my-nginx
helm get all my-nginx
helm get values my-nginx
helm show values bitnami/nginx

```
🧱 **Chart Management**

```
# Create a new chart
helm create mychart

# Directory structure
mychart/
├── Chart.yaml          # Chart metadata
├── values.yaml         # Default config values
├── templates/          # K8s manifests
│   ├── deployment.yaml
│   ├── service.yaml
│   └── _helpers.tpl
└── charts/             # Dependencies

```

⚙️ **Chart.yaml Example**

```
apiVersion: v2
name: mychart
description: A sample Helm chart
type: application
version: 1.0.0
appVersion: "1.16.0"

```

---

### 🧩 **values.yaml Example**

```
replicaCount: 3

image:
  repository: nginx
  tag: latest
  pullPolicy: IfNotPresent

service:
  type: LoadBalancer
  port: 80
```

---
### 🧰 **Templating Syntax**

In `templates/deployment.yaml`:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-deployment
spec:
  replicas: {{ .Values.replicaCount }}
  template:
    spec:
      containers:
      - name: {{ .Chart.Name }}
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
        ports:
        - containerPort: {{ .Values.service.port }}
```


Render YAMLs without applying:
```
helm template my-nginx bitnami/nginx
```

---

### 🧩 **Upgrade Strategies**

|Command|Description|
|---|---|
|`helm upgrade --install`|Installs if not already deployed.|
|`helm diff upgrade`|Shows changes before upgrading (requires plugin).|
|`helm rollback`|Restores previous release version.|

---

### 🔐 **Helm Secrets**

Use plugins like **helm-secrets** to encrypt secrets with **SOPS/KMS**:


```
helm secrets enc values.yaml
helm secrets dec values.yaml
helm secrets install myapp ./chart -f secrets.yaml

```

---

### 📦 **Dependency Management**

Add dependencies inside `Chart.yaml`:

```
dependencies:
  - name: redis
    version: 17.0.0
    repository: https://charts.bitnami.com/bitnami
```

Then
```
helm dependency update
```

---

### 🧭 **Helm + GitOps (ArgoCD)**

- ArgoCD can directly deploy **Helm charts** from Git repositories.
    
- You specify:


```
spec:
  source:
    repoURL: https://github.com/example/helm-repo.git
    path: charts/myapp
    targetRevision: main
    helm:
      valueFiles:
      - values-prod.yaml

```

Enables **declarative Helm deployment** with version control.

---

### 🧠 **Best Practices**

- Keep **values.yaml** simple and environment-specific (values-dev.yaml, values-prod.yaml).
    
- Use **Helm lint** to validate chart structure:

```
helm lint ./mychart
```
- Use **semantic versioning** in `Chart.yaml`.
    
- Store **charts in private repositories** (e.g., S3, Nexus).
    
- Combine with **ArgoCD** or **FluxCD** for GitOps-based deployment.
    
- Always **template before apply** (`helm template`) to validate generated manifests.
---

### 🧾 **Useful Plugins**

|Plugin|Use|
|---|---|
|**helm-diff**|Shows what will change during upgrade.|
|**helm-secrets**|Encrypts/decrypts secrets.|
|**helm-unittest**|Adds test cases for Helm templates.|

---

### ⚡ **Quick Reference Commands**


```
helm create mychart
helm lint mychart
helm template mychart
helm install myapp ./mychart
helm upgrade myapp ./mychart
helm uninstall myapp
helm repo add bitnami https://charts.bitnami.com/bitnami
helm search repo nginx
helm list -A
helm rollback myapp 2

```






