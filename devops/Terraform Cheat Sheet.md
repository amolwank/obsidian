# 🚀 Terraform Senior-Level Interview Cheat Sheet

---

## 1. **Core Concepts**

- **Providers** → Plugins to manage resources (AWS, GCP, Azure, Kubernetes, etc.).
    
- **Resources** → Actual infrastructure objects (e.g., `aws_instance`).
    
- **Data Sources** → Fetch existing info (`data "aws_vpc"`).
    
- **Modules** → Reusable groups of resources.
    
- **State** → Source of truth for infra, stored locally or remotely.
    
- **Backend** → Stores state remotely (S3 + DynamoDB lock).
    
- **Variables & Outputs** → Inputs for flexibility, outputs for sharing info.
    

**Q:** What’s the difference between `resource` and `data`?  
👉 `resource` creates infra, `data` reads existing infra.

---

## 2. **State Management**

- **Remote State** → S3 + DynamoDB lock (team collaboration).
    
- **State Locking** → Prevents race conditions.
    
- **Terraform Refresh** → Syncs state with reality.
    
- **Drift Detection** → Run `plan` often to detect changes outside Terraform.
    

**Q:** How do you secure Terraform state?  
👉 Store in S3 with SSE, use DynamoDB for locking, restrict access with IAM.

---

## 3. **Modules**

- **Root module:** Main entry (env level – dev, prod).
    
- **Child modules:** Reusable building blocks.
    
- **Registry modules:** Pre-built modules for AWS, GCP, etc.
    
- **Best practices:** Keep generic, versioned, documented.
    

**Q:** How do you structure Terraform code?  
👉 Root modules per environment → reusable child modules → remote backend → workspaces for isolation.

---

## 4. **Workspaces**

- **Purpose:** Manage multiple environments (`dev`, `stage`, `prod`) with same config.
    
- **Limitations:** Not ideal for big orgs; prefer separate state files per env.
    

---

## 5. **Provisioners (Avoid When Possible)**

- `local-exec` & `remote-exec`.
    
- Not idempotent; prefer using configuration management (Ansible, Packer).
    

---

## 6. **Terraform Lifecycle**

- `create_before_destroy` → Ensures HA during replacement.
    
- `prevent_destroy` → Prevent accidental deletion (use on DBs).
    
- `ignore_changes` → Ignore external changes.
    

---

## 7. **Terraform CLI Commands**

- `terraform init` → Init provider/backend.
    
- `terraform plan` → Show execution plan.
    
- `terraform apply` → Apply changes.
    
- `terraform destroy` → Tear down infra.
    
- `terraform fmt` → Format code.
    
- `terraform validate` → Check syntax.
    
- `terraform import` → Bring existing infra under Terraform.
    
- `terraform taint` → Force recreate resource.
    
- `terraform graph` → Dependency visualization.
    

---

## 8. **Best Practices**

- Use **remote state** + locking.
    
- Separate **environments** (dev, stage, prod).
    
- Use **modules** for reusability.
    
- Use **version pinning** for providers/modules.
    
- Run **terraform plan** in CI/CD, require approval for apply.
    
- Store secrets in **AWS Secrets Manager/SSM**, not in TF code.
    

---

## 9. **Interview Scenarios**

**Q1:** How do you manage Terraform in a team?  
👉 Use remote state (S3+DynamoDB), Git for code, PR reviews, Terraform Cloud or CI/CD for apply.

**Q2:** How do you handle sensitive variables?  
👉 Use `sensitive = true`, pass via environment variables or secret manager, never commit to Git.

**Q3:** How do you avoid downtime during deployments?  
👉 Use `create_before_destroy`, rolling updates (ASG), blue/green for critical infra.

**Q4:** How do you handle drift?  
👉 Run `terraform plan`, compare with actual infra, fix manually or re-apply.

---

## 10. **Advanced Topics**

- **Terraform Cloud/Enterprise**: Remote execution, RBAC, Sentinel policies.
    
- **Policy as Code:** [[Sentinel]] or OPA to enforce compliance (e.g., no public S3).
    
- **Dynamic Blocks:** For repetitive nested configs.
    
- **for_each vs count:**
    
    - `count` → index-based, good for identical resources.
        
    - `for_each` → key-based, better for sets/maps.
        

---

## 🔑 Quick Reminders for Interviews

- **Terraform is declarative** (define desired state, TF makes it happen).
    
- Always mention **Idempotency** (apply = same result, no duplicates).
    
- Terraform follows **execution graph** (resource dependencies).
    
- For **multi-region/multi-account**, use **workspaces + remote state + modules**.