👉 If a developer **removes a resource from the Terraform code but not from AWS**, here’s what happens:

- **Terraform Plan**
    - During `terraform plan`, Terraform compares the code (desired state) with the state file and the actual AWS resources.
    - Since the resource is missing in code but exists in state, Terraform marks it for **deletion**.
        
- **Terraform Apply**
    - On running `terraform apply`, Terraform will **delete the resource from AWS** to match the new desired state (which no longer includes that resource).

---

✅ **Key Point to Remember**  
Terraform follows **"code is the source of truth"**.  
If it's not in the code → Terraform assumes it shouldn’t exist → it will delete it.

---

⚡️ **Best Practices to Avoid Accidental Deletion**
- Enable `deletion_protection` on critical resources (like RDS, S3).
- Use `lifecycle { prevent_destroy = true }`.
- Require code reviews and `terraform plan` approvals in CI/CD before apply.