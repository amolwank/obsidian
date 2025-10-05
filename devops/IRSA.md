IRSA stands for IAM Roles for Service Accounts in AWS.

It's a way to let Kubernetes pods running on Amazon EKS securely access AWS services (like S3, DynamoDB, SQS, etc) without needing to store AWS credentials inside the pod.

How IRSA works?
1. You create an IAM Role with the necessary AWS permissions.
2. You  links that IAM Role to a Kubernetes Service Account using an annotation.
3. When a pod runs under that Service Account, AWS automatically provides Temporary credential via the EKS OIDC (OpenID Connect ) provider.
4. The pod can then securely call AWS APIs (e.g. read/write to S3) without storing access keys.

Why IRSA is Useful:
- No hardcoded secrets -> avoids storing AWS access keys in config files or environment variables.
- Fine-grained permissions -> You can assign different roles to different service accounts (least privilege)
- Automatic credential rotation -> AWS handles temporary credentials securely.
- Kubernetes-native -> integrates directly with service accounts.

### **What is IRSA?**

- **IRSA (IAM Roles for Service Accounts)** allows a **Kubernetes pod** to assume an **AWS IAM role** securely.
- This provides **fine-grained permissions** to pods without using long-lived AWS credentials.
- It’s the recommended way to give pods access to AWS services like S3, DynamoDB, or SNS.

---
### **How it Works**
1. Create an **IAM Role** with a trust policy for **EKS OIDC provider**.
2. Create a **Kubernetes Service Account** and annotate it with the IAM Role ARN.
3. Pods using this service account automatically assume the IAM Role.
    

**Architecture Flow:**
```
Pod → Kubernetes ServiceAccount → IAM Role (via OIDC) → AWS API
```

### **Example Use Case**

- Pod needs to read from an S3 bucket.
- Instead of embedding AWS keys, attach an IAM Role to the pod via IRSA.
- Kubernetes automatically provides temporary credentials to the pod.
---
### **Interview-Ready Answer (30–40 sec)**

_"Yes, I have used IRSA in AWS EKS. It allows Kubernetes pods to assume AWS IAM roles securely using the OIDC provider. I create an IAM role with the required AWS permissions and annotate the Kubernetes Service Account with the role ARN. Pods using this Service Account automatically get temporary credentials, eliminating the need for hardcoded keys and enabling fine-grained access to AWS services like S3 or DynamoDB."_

Video Ref: https://www.youtube.com/watch?v=fSOwXvZOzRI
