## 🔑 **Significance of `source` in Terraform Modules**

1. **Defines module location**
    
    - The `source` specifies **where Terraform should pull the module code from** (local path, remote repo, registry, etc.).
        
    - Without `source`, Terraform doesn’t know which module to use.
        
2. **Enables reusability**
    
    - Instead of rewriting the same `.tf` resources multiple times, you can keep them in a module and call it using `source`.
        
    - Makes infra more **modular, reusable, and maintainable**.
        
3. **Supports multiple backends (flexible sources)**
    
    - You can fetch modules from:
        
        - **Local path** → `"../vpc"`
            
        - **Terraform Registry** → `"terraform-aws-modules/vpc/aws"`
            
        - **Git repository** → `"git::https://github.com/org/repo.git//modules/vpc?ref=tag"`
            
        - **S3 / GCS / HTTP URL**
            
4. **Version control**
    
    - Using `source` with version constraints (when supported) ensures consistency.
        
    - Example (Terraform Registry):
```
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.0.0"
}
```

**Isolation of environments**

- You can reuse the same module across **dev, stage, prod** simply by pointing `source` to the same module but with different `tfvars`.

```
module "network" {
  source = "../modules/vpc"
  cidr_block = "10.0.0.0/16"
}
```
Remote (Terraform Registry)
```
module "s3_bucket" {
  source  = "terraform-aws-modules/s3-bucket/aws"
  version = "3.8.2"
  bucket  = "my-app-bucket"
}
```
GitHub repo

```
module "eks" {
  source = "git::https://github.com/terraform-aws-modules/terraform-aws-eks.git?ref=v20.8.5"
}
```

## ✅ Interview-friendly Summary

- The **`source` in a Terraform module block tells Terraform where to get the module code**.
- It enables **code reusability, consistency, and modular infrastructure design**.
- Sources can be **local, registry, Git, or cloud storage**.
- Adding a `version` lock ensures predictable builds.