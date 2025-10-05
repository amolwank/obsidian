## 🔹 How to Prevent Direct `terraform apply` from Laptops

### 1. **Centralize Execution**

- Only allow **CI/CD pipelines (GitHub Actions, Jenkins, GitLab CI)** to run `terraform apply`.
- Developers can run `terraform plan` locally, but not apply.
    

---

### 2. **IAM Permissions**

- Developers get **read-only or plan-only IAM roles**.    
- Only CI/CD runner service role has **apply permissions** (e.g., `ec2:Create*`, `s3:Put*`).
- Enforce via **IAM policies** + AWS SSO/AWS Organizations.

---

### 3. **Remote State & Locks**

- Store state in **S3 + DynamoDB** (or Terraform Cloud).    
- Configure **state locking** so laptop applies can’t override pipeline applies.
    

---

### 4. **Terraform Cloud/Enterprise (Optional)**

- Use **Terraform Cloud/Enterprise** with policy-as-code (Sentinel/OPA).    
- Enforce that all applies go through TFC — block CLI applies.
    

---

### 5. **Git Workflow**

- Infra changes must go through **PR reviews** → pipeline → controlled apply.    
- Protect `main` branch (no direct pushes).
    

---

## 🔹 Interview-Ready Answer (45 sec)

_"We ensure developers don’t run `terraform apply` directly by restricting IAM permissions — developers have read-only or plan-only roles, while only our CI/CD pipeline role can apply changes. The Terraform state is stored remotely in S3 with DynamoDB locking, so even if someone tries locally, they can’t override the pipeline. All infra changes go through pull requests, code review, and automated GitHub Actions pipelines. This enforces consistency, auditability, and prevents accidental production changes."_

