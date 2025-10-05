
## 🔹 How to Roll Back a Broken Module Update

### 1. **Version Pinning (Best Practice)**

- Always use **versioned modules** (Git tag / registry version).
    
- If `v2.3.0` breaks infra → rollback to `v2.2.1`.
```
module "eks" {
  source  = "git::https://github.com/org/terraform-modules.git//eks?ref=v2.2.1"
}
```
### 2. **Revert Code Change**

- In Git, revert the PR/commit that bumped the module version.
    
- Push → CI/CD reruns → Terraform detects drift → restores infra to the old working config.
    

---

### 3. **Terraform Plan & Apply**

- Run `terraform plan` → confirm rollback changes.
    
- Run `terraform apply` → infra is restored to the previous working state.
    

---

### 4. **Use Remote State**

- Since state is stored in **S3 + DynamoDB** or Terraform Cloud, rolling back is **safe and consistent across teams**.
    

---

### 5. **If Infra is Already Broken**

- If rollout partially applied →
    
    - Use `terraform apply -refresh-only` to re-sync state.
        
    - Or manually **import unchanged resources** before re-applying.
        
- If severe, restore from **backups** (e.g., DB snapshots, AMI images).
    

---

## 🔹 Interview-Ready Answer (40 sec)

_"If a module update breaks production, I would immediately roll back by reverting to the last known good module version. Since we pin module versions using Git tags, I can simply update the source back to the stable version and reapply Terraform. We always run `terraform plan` before apply to confirm rollback actions. Additionally, remote state in S3/DynamoDB ensures consistency, so rollback is safe across teams. For critical resources like databases, we rely on AWS backups and snapshots as an extra safety net."_
