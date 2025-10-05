### ⏱️ **30-second answer (short)**

“I’d enforce compliance with **policy-as-code** tools like HashiCorp Sentinel or Open Policy Agent (OPA) with Conftest/OPA Gatekeeper. Additionally, I use pre-commit hooks and CI/CD checks to block unencrypted S3 buckets before they’re applied.”

---

### ⏱️ **60-second answer (structured)**

“To ensure compliance, I put guardrails at multiple levels:

- **Terraform modules** → Define S3 encryption inside shared modules, so teams can’t bypass it.
    
- **Policy as Code** → Use Sentinel (Terraform Cloud) or OPA/Conftest in CI/CD to check for required encryption settings.
    
- **Pre-commit hooks** → Run `terraform validate` and `tflint` locally before commits.
    
- **CI/CD enforcement** → GitHub Actions pipeline rejects PRs if rules fail.  
    This guarantees that every bucket is encrypted before reaching production.”
    

---
✅ **Memory Trick** → Think **M-P-C**:

- **Modules** → default encryption
    
- **Policy** → Sentinel/OPA
    
- **CI/CD** → block bad code
    

---