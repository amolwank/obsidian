### 🧩 What is **EKS OIDC Provider**?

- **OIDC** stands for **OpenID Connect**, an identity layer built on top of OAuth 2.0.
    
- In **Amazon EKS**, an **OIDC provider** allows your Kubernetes pods to **authenticate with AWS services** **without** needing to store long-term IAM credentials (like access keys) inside the pod.
    

---

### 🏗️ Why it’s used

Normally, AWS IAM Roles are attached only to EC2 instances.  
With OIDC (OpenID Connect), **EKS can issue temporary credentials directly to pods** using **IAM Roles for Service Accounts (IRSA)**.

So instead of giving the whole node access → only the specific pod/service account gets permissions.

---

### 🔐 How it Works (Flow)

1. You **enable the OIDC provider** for your EKS cluster.  
    This creates a trust relationship between IAM and your EKS OIDC endpoint.
    
2. You **create an IAM role** that trusts this OIDC provider.
    
3. You **annotate your Kubernetes service account** with that IAM role ARN.
    
4. When the pod runs with that service account, it automatically gets **temporary credentials** for the IAM role.