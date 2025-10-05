## 🔄 **State Drift**

- **Drift** happens when the **real infrastructure** is changed **outside of Terraform** (manual changes in AWS Console/CLI/other tools).
    
- Example:
    
    - Terraform state says an EC2 instance has size `t2.micro`.
        
    - Someone manually changes it to `t3.medium` in AWS.
        
    - Now **state ≠ reality** → that’s drift.
        

👉 Terraform will detect drift the next time you run `terraform plan` or `terraform refresh`.

---

## 🔄 **terraform refresh** (Terraform v0.15 and earlier – replaced by `terraform apply/plan` in newer versions)
```
terraform refresh
```

- Purpose: Updates the **state file** to match the **real infrastructure**.
    
- Example: If the EC2 instance was changed to `t3.medium` manually, running `terraform refresh` updates the state file to reflect that.
    

⚠️ Important: `refresh` **doesn’t fix drift**. It just **updates the state**. If you want to fix it (make infra match code), you run:
```
terraform apply
```

📖 Simple Analogy

    State Drift → Someone moved your furniture when you weren’t looking.

    Refresh → Updating your house map to show the new furniture positions.

    Apply → Moving furniture back to match your blueprint.

📝 Easy line to remember

“State drift means infra and state are out of sync. terraform refresh updates the state file with actual infra details, but only terraform apply brings infra back in sync with code.”

### 🕐 **30-sec Answer**

“State drift happens when infrastructure is changed outside of Terraform, so the state file and real resources don’t match. `terraform refresh` updates the state file with the actual resource details, while `terraform apply` ensures the infrastructure matches the code again.”

---

### 🕐 **60-sec Answer**

“Terraform uses the state file as its source of truth. If someone manually changes infrastructure outside Terraform, that creates drift. For example, Terraform says an EC2 is `t2.micro` but it’s manually changed to `t3.medium`. To handle this, `terraform refresh` updates the state file to reflect the real infrastructure, but it doesn’t fix drift. If you want to bring infrastructure back in line with your Terraform code, you run `terraform apply`.”

---

### 🕐 **Detailed Answer**

“State drift occurs when there’s a mismatch between the Terraform state file and the actual infrastructure, usually due to manual changes outside of Terraform. This can cause inconsistencies during deployments. `terraform refresh` is used to update the state file so Terraform knows the current reality of resources. However, it doesn’t modify the infrastructure. If you want your infrastructure to strictly match what’s written in the Terraform code, you need to run `terraform apply` after refresh, which reconciles drift by enforcing the code-defined state.”