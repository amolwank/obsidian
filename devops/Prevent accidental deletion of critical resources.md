### ⏱️ **30-second answer (concise)**

“I use `lifecycle { prevent_destroy = true }` in Terraform for critical resources like RDS and S3. This blocks accidental `terraform destroy`. Additionally, I enforce resource policies and IAM permissions so only pipelines, not developers, can apply changes.”

---

### ⏱️ **60-second answer (structured)**

“To prevent accidental deletion, I combine multiple safeguards:

- In Terraform → I add `lifecycle.prevent_destroy = true` for RDS and S3.
- In AWS → I enable S3 bucket versioning and MFA delete, and for RDS, I enable final snapshots before deletion.
- In IAM → I restrict destructive actions to CI/CD pipelines, not developers’ laptops.
- In Process → All changes go through PR + `terraform plan` review before apply.
    
This way, even if someone pushes a bad config, critical infra can’t be deleted directly.”

---

### 📖 **Detailed (2–3 min)**

“If we’re running production-critical workloads, accidental deletion is a huge risk. Terraform gives us **lifecycle policies**:

```
resource "aws_s3_bucket" "critical_data" {
  bucket = "prod-critical-data"

  lifecycle {
    prevent_destroy = true
  }
}
```
This prevents `terraform destroy` from removing the bucket.

For RDS:

- I use `prevent_destroy`
- I enforce **final snapshots** on deletion.
- I use **multi-AZ + backups** so even if deletion is forced, data is safe.

On the AWS side:
- I enable **S3 versioning + MFA Delete**.
- Use **Service Control Policies (SCPs)** in AWS Organizations to block destructive API calls for production accounts.

On the process side:

- All Terraform applies go via **GitHub Actions pipelines**, not local laptops.    
- Every `terraform plan` is peer-reviewed in a Pull Request before apply.

This defense-in-depth approach ensures no single mistake wipes out critical infra.”

---

✅ **Easy way to remember** → Think of 3 layers:

- **Terraform** (prevent_destroy)
- **AWS features** (versioning, final snapshot, MFA delete)
- **Process** (CI/CD + reviews)