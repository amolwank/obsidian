
### What is self-hosted runner in github actions
#### 🔹 **Self-Hosted Runner in GitHub Actions**

- By default, GitHub Actions uses **GitHub-hosted runners** (like `ubuntu-latest`, `windows-latest`, `macos-latest`).
- A **self-hosted runner** is a server (your own VM, EC2 instance, on-prem server, even a Kubernetes pod) that you configure to run GitHub Actions jobs.

---

#### 🔹 **Why use self-hosted runners?**

- **Custom environment:** Install custom tools, SDKs, or dependencies not available in GitHub-hosted runners.
- **Private networking:** Access internal resources (databases, private APIs, VPC-only services).
- **Performance/cost:** Avoid per-minute billing of GitHub-hosted runners if you already have infra.
- **Compliance:** Keep builds inside your own infra for security/regulatory reasons.
    

---

#### 🔹 **How it works**

1. You register a machine as a runner in your repo/org via GitHub.
    
2. Install the **GitHub Actions runner application** on that machine.
    
3. In your workflow, specify:
```
runs-on: self-hosted
```
 1. Jobs are then executed on your machine instead of GitHub’s.
### **What is Kubernetes API?**

- The **Kubernetes API** is the **central control plane interface** that all components and users interact with to manage the cluster.
- Everything in Kubernetes — pods, services, deployments, configmaps, secrets — is represented as an **API object**, and all operations are performed via the API.
- The API is **RESTful** and uses **JSON/YAML** over HTTP(S).
#### **Interview-Ready Answer (30–40 sec)**

_"The Kubernetes API is the central interface for managing a cluster. Every resource in Kubernetes — pods, deployments, services, secrets — is represented as an API object. Tools like kubectl, Helm, Terraform, and controllers communicate with the API to create, update, or delete resources. The API enforces authentication and RBAC-based authorization, and all cluster state is stored in etcd. Essentially, the API is the single source of truth for the cluster."_

#### ConfigMap vs Secretes:
Here’s a clear explanation of **ConfigMap vs Secret** in Kubernetes — perfect for interviews:

---

|Feature|**ConfigMap**|**Secret**|
|---|---|---|
|**Purpose**|Store **non-sensitive configuration data**|Store **sensitive data** (passwords, tokens, keys)|
|**Data Storage**|Base64 encoded (not encrypted by default)|Base64 encoded (can enable encryption at rest)|
|**Examples**|App config, URLs, environment variables|DB passwords, API keys, TLS certificates|
|**Access**|Mounted as **volume** or environment variables|Mounted as **volume** or environment variables|
|**Security**|Less sensitive, no extra encryption by default|Can be encrypted in etcd, supports RBAC and encryption policies|
|**Use Case**|App configuration that is safe to expose|Credentials or secrets that must remain confidential|
### **Key Points for Interviews**

1. **ConfigMap** is for **regular config data**; Secrets are for **sensitive information**.
2. Both can be mounted as **environment variables** or **volumes** inside pods.
3. Secrets can be encrypted in etcd for security, ConfigMaps are generally not.
4. Using Secrets ensures sensitive info is **not hardcoded** in images or manifests.
---
### **Interview-Ready Answer (30–40 sec)**
_"A ConfigMap in Kubernetes stores non-sensitive configuration data, like URLs or app settings, whereas a Secret stores sensitive information, like passwords, API keys, or certificates. Both can be injected into pods via environment variables or volumes, but Secrets provide encryption options and are treated securely by Kubernetes, whereas ConfigMaps are not encrypted by default."_