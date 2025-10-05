Nice — there are several ways to give EKS workloads access to S3. The **recommended** and modern approach is **IRSA (IAM Roles for Service Accounts)**. I’ll explain IRSA first (with concrete examples you can apply immediately), then list alternatives and network-level hardening (VPC endpoints + bucket policies).

---

# 1) Recommended — **IRSA (IAM Role for Service Account)**

**Why:** gives least-privilege, per-service-account credentials, no static keys, uses short‑lived web‑identity tokens provided by the cluster OIDC provider.

### High level steps

1. Enable/create the EKS OIDC provider for your cluster.
    
2. Create an IAM role with a trust policy that allows the OIDC provider and a specific Kubernetes service account to assume the role.
    
3. Attach an S3 permissions policy to that IAM role.
    
4. Create a Kubernetes ServiceAccount with the annotation pointing to that IAM role.
    
5. Pods using that ServiceAccount will retrieve temporary credentials automatically via the AWS SDK.
    

---

### Example IAM policy (allow read-only to a specific bucket)

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowReadFromMyBucket",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::my-app-bucket",
        "arn:aws:s3:::my-app-bucket/*"
      ]
    }
  ]
}
```

Kubernetes ServiceAccount (annotate with the IAM role ARN)
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "arn:aws:iam::AWS_ACCOUNT_ID:oidc-provider/oidc.eks.<region>.amazonaws.com/id/<OIDC_ID>"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringEquals": {
          "oidc.eks.<region>.amazonaws.com/id/<OIDC_ID>:sub": "system:serviceaccount:my-namespace:my-serviceaccount"
        }
      }
    }
  ]
}
```

Pod example (uses the service account)
```
apiVersion: v1
kind: Pod
metadata:
  name: s3-client
  namespace: my-namespace
spec:
  serviceAccountName: my-serviceaccount
  containers:
  - name: app
    image: amazonlinux
    command: ["sh","-c","yum install -y python3 && python3 -c 'import boto3,os; s3=boto3.client(\"s3\"); print(s3.list_objects(Bucket=\"my-app-bucket\"))'"]
```

The AWS SDK inside the container will automatically use the web identity token and STS to get temporary credentials for the IAM role.

---

# 2) Alternative — **Node IAM Role (Instance profile)**

- Attach an IAM role to the worker nodes (EC2 instance profile). All pods on the node share those node credentials unless you implement per-pod controls.
    
- Simpler, but **less secure** (co-tenancy risks): any pod on the node could potentially access S3 if it can access the instance metadata (IMDS) or environment.
    

---

# 3) Legacy tools — **kube2iam / kiam**

- These intercept metadata requests and provide per-pod IAM roles. They were popular before IRSA.
    
- More moving pieces and extra network hops — IRSA is preferred now.
    

---

# 4) Bad options (don’t use in prod)

- **Static AWS access keys** stored as k8s Secrets or env vars — risk of leakage and no rotation.
    
- **Embedding creds in images** — insecure.
    

---

# 5) Network-level hardening (S3 VPC Endpoint & Bucket Policy)

Even with proper IAM, you can limit where S3 access can originate.

### VPC Endpoint (Gateway) for S3

- Create a VPC Gateway Endpoint for S3 so traffic to S3 stays within the AWS network (no NAT/Internet).
    

### Example S3 bucket policy that limits access to a specific IAM role (and optional VPC endpoint)

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowRoleToGetObjects",
      "Effect": "Allow",
      "Principal": { "AWS": "arn:aws:iam::AWS_ACCOUNT_ID:role/my-eks-s3-role" },
      "Action": [ "s3:GetObject", "s3:ListBucket" ],
      "Resource": [
        "arn:aws:s3:::my-app-bucket",
        "arn:aws:s3:::my-app-bucket/*"
      ]
    },
    {
      "Sid": "DenyIfNotFromVpcEndpoint",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": ["arn:aws:s3:::my-app-bucket","arn:aws:s3:::my-app-bucket/*"],
      "Condition": {
        "StringNotEquals": {
          "aws:sourceVpce": "vpce-0123456789abcdef0"
        }
      }
    }
  ]
}
```

- This enforces that only the specific IAM role can access the bucket, and optionally denies requests not coming through the VPC endpoint.
    

---

# 6) Best practices summary

- Use **IRSA** for per-workload least-privilege access.
    
- Give the IAM role only the exact S3 permissions needed (narrow resource ARNs).
    
- Use **VPC endpoint** for S3 to avoid internet egress.
    
- Apply **bucket policies** to restrict by role and/or VPC endpoint.
    
- Avoid static keys and avoid using node instance profiles for multi-tenant clusters.
    
- Enable logging (S3 server access logs / CloudTrail) to monitor access.
    

---

If you want, I can:

- generate the exact `aws iam create-role` trust policy + policy JSON and the kubernetes YAML for IRSA, **or**
    
- produce a Terraform module that creates the OIDC provider, IAM role, S3 policy, and annotated ServiceAccount — tell me which and I’ll provide it right away.
