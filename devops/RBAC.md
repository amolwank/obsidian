
**RBAC ( (Role-Based Access Control)** )In Kubernetes:
Kubernetes uses RBAC to control who can do what in the cluster.
- Role -> Defines a set of permissions (like "can list pods", or "can create deployments").
- ClusterRole -> Same as Role but cluster-wide.
- RoleBinding -> Assign s Role to a user/service account in a namespace.
- ClusterRoleBinding -> Assigns a ClusterRole to a user/service account across the whole cluster.
### **What is RBAC?**

- **RBAC (Role-Based Access Control)** is a **mechanism to control who can do what in a Kubernetes cluster**.
- It defines **permissions** (verbs) for **users, groups, or service accounts** on **resources** (pods, deployments, secrets, etc.).
- Helps enforce the **principle of least privilege**.
### **Core Components of RBAC**

|Component|Purpose / Description|
|---|---|
|**Role**|Defines **namespace-scoped permissions** (verbs on resources)|
|**ClusterRole**|Defines **cluster-wide permissions** or can be namespace-specific|
|**RoleBinding**|Grants a Role to a **user, group, or ServiceAccount** within a namespace|
|**ClusterRoleBinding**|Grants a ClusterRole to a user, group, or SA **cluster-wide**|
example
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: dev
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

- `my-app-sa` can **get, watch, and list pods** in the `dev` namespace only.
    

---

### **Interview-Ready Answer (30–40 sec)**

_"RBAC in Kubernetes is Role-Based Access Control, used to define who can do what on which resources. Roles and ClusterRoles define permissions, while RoleBindings and ClusterRoleBindings assign these permissions to users, groups, or service accounts. It ensures least-privilege access, so pods or users can only perform allowed actions, enhancing security and governance in the cluster."_