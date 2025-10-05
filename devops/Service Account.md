#### **What is a Service Account?**

- A **Service Account (SA)** is an identity for **processes running inside Kubernetes pods**.
- It allows pods to **authenticate to the Kubernetes API** and access resources securely.
- Every pod can either use the **default service account** in its namespace or a **custom service account**.

##### **Key Uses of Service Accounts**

1. **Pod Authentication:**
    - Pods use a service account token to communicate with the Kubernetes API.
2. **RBAC Permissions:**
    - Service accounts are tied to **RoleBindings** or **ClusterRoleBindings** to control **what a pod can do** (read/write configmaps, secrets, pods, etc.).
3. **Secret Management:**
    - Kubernetes automatically mounts a **token and CA certificate** for the service account in the pod, enabling secure API access.
4. **External Integrations:**
    - Service accounts can be linked with **IAM roles in AWS (IRSA)** or other cloud identities for pod-to-cloud service access.


#### Custom Service Account:
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-app-sa
  namespace: dev
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: dev
subjects:
- kind: ServiceAccount
  name: my-app-sa
  namespace: dev
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
**Explanation:**

- Pod using `my-app-sa` can **only read pods** in the `dev` namespace.
    

---

### **Interview-Ready Answer (30–40 sec)**

_"A Service Account in Kubernetes provides an identity for pods to access the Kubernetes API securely. It allows assigning **fine-grained permissions** using RBAC, so pods can only perform allowed actions. It also automatically mounts a token and certificate inside the pod. Service Accounts are essential when pods need to access secrets, configmaps, or even external cloud resources like AWS via IRSA."_

A service account (SA) is a special type of identity used by applications, services, or workloads (not humans) to interact with a system securely.

Service Account In Kubernetes:
- In Kubernetes, a Service Account is used by pods to talk to the Kubernetes API. 
- Each pod runs as a service account by default (default SA).
- You can create custom service accounts and give them RBAC roles for fine-grained access.