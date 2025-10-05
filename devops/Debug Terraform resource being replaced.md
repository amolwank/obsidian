### 🔍 Debugging Unexpected Resource Replacements in Terraform

When you see a resource being **replaced** (`-/+` in plan), here’s how to debug:

1. **Check the `terraform plan` diff carefully**
    - Look for which **arguments changed**.
    - Example: AMI ID, subnet ID, or `force_new_deployment` flags often trigger replacement.
        
2. **Understand which attributes are `ForceNew`**
    - Some resource arguments (like `instance_type` for EC2, `engine_version` for RDS) **require replacement** by design.
    - Docs for each resource list which fields are `ForceNew`.
        
3. **Check for drift in real infra**
    - Run `terraform refresh` or `terraform plan -refresh-only`.
    - Sometimes resources drift in AWS (e.g., a tag added manually), and Terraform wants to reconcile.
        
4. **Check data sources & dependencies**
    
    - If a data source (like `data.aws_ami.latest`) always fetches a new value, Terraform sees it as a change
    - Fix by **pinning versions** (e.g., AMI ID instead of `latest`).
        
5. **Look at lifecycle rules**
    - Add `lifecycle { ignore_changes = [tags] }` if non-critical fields (like tags or userData) keep changing.
        
6. **Check module or provider version changes**
    
    - Upgrading the AWS provider or a module might introduce new defaults → Terraform thinks something changed.

---

### ✅ Best Practices to Prevent Future Surprises

- Pin AMIs instead of using `latest`.    
- Use `ignore_changes` for fields managed outside Terraform.
- Add `prevent_destroy` for critical resources.
- Use `terraform plan` in PRs so team can review replacements before apply.

---

👉 **Memory trick**:  
Think **"Why Replace?" = ForceNew, Drift, Defaults, Data Sources, Lifecycle.**  
(5 keywords to recall in interviews 🚀)