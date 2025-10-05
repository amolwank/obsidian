### **Scenario:**

👉 Multiple teams, same AWS account → risk of **Terraform state conflicts** if everyone shares a single state file.

---

### **Answer Approach (Step-by-Step):**

1. **Remote Backend for Centralized State**
    - Store Terraform state in **S3 backend** with **DynamoDB table for locking**.
    - Ensures that only one `terraform apply` can run at a time, avoiding race conditions.   
2. **State Separation by Teams/Projects**
    - Don’t keep _all_ resources in a single state file.
    - Split into **multiple state files** (per team, per environment, or per service).
    - Example: Networking team manages VPC state, Application team manages ECS/EKS state, Data team manages RDS state.    
3. **Naming Conventions**
    - Use clear **S3 key prefixes** for each team:
	    - bucket: terraform-states
	    - key: networking/prod/terraform.tfstate
	    - key: app/prod/terraform.tfstate
	    - key: data/dev/terraform.tfstate 
4. **Workspaces for Environments**
    - Use **Terraform workspaces** or separate state files for `dev`, `stage`, `prod`.
    - Prevents accidental cross-environment modifications.
5. **Access Control**
    - Apply **IAM permissions** so each team can only access their state file in S3.
    - Enforce RBAC so one team can’t override another’s resources.
---
### **Interview-Ready Answer (45–60 sec)**
_"If multiple teams are working in the same AWS account, I avoid conflicts by using a remote backend like S3 with DynamoDB locking, so only one Terraform operation can run at a time. I split the infrastructure into separate state files — for example, networking, application, and data — so teams manage their own resources independently. Each state file is stored with unique S3 key prefixes, and we use workspaces or separate backends for dev, stage, and prod. On top of that, IAM permissions ensure teams only access their relevant state. This approach prevents conflicts, enforces isolation, and keeps deployments safe and scalable."_