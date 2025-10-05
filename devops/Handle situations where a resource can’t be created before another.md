### ⏱️ **30-second answer (concise)**

“I use Terraform’s `create_before_destroy` lifecycle rule so the new resource is provisioned first before destroying the old one. If it’s a resource that can’t coexist, I use strategies like `terraform taint`, manual steps, or blue/green approaches to minimize downtime.”

---

### ⏱️ **60-second answer (structured)**

“In Terraform, some resources — like Elastic IPs, databases, or load balancers — can’t be created if the old one exists. To handle this:

- I use `lifecycle { create_before_destroy = true }` when both versions can exist temporarily.
    
- If coexistence isn’t possible, I plan a **blue/green deployment** — creating parallel infra, switching traffic, then destroying old infra.
    
- For truly singleton resources (like RDS), I sometimes do manual imports, snapshot/restore, or use `terraform taint` to force recreation safely.  
    This ensures minimal downtime and safe transitions.”
    

---

### 📖 **Detailed (2–3 min)**

“This happens often with resources that don’t allow duplicate names or have hard dependencies, like:

- S3 bucket names (globally unique)
    
- RDS instances with unique identifiers
    
- IAM roles with fixed names
    

**Strategies I use:**

1. **Lifecycle Rule – Preferred**
```
resource "aws_instance" "web" {
  ami           = "ami-123"
  instance_type = "t2.micro"

  lifecycle {
    create_before_destroy = true
  }
}

```
This tells Terraform: bring up the new instance, then destroy the old one.

2. **Name Randomization**
    
    - Append random suffixes so new resources can be created without naming conflict.
        
3. **Blue/Green or Parallel Infra**
    
    - Stand up new infra in parallel → switch DNS/Load Balancer → destroy old.
        
4. **Manual Import/State Move**
    
    - Import existing resources or move state references (`terraform state mv`) if replacement isn’t possible.
        
5. **Last Resort**
    
    - Use `terraform taint` to force recreation or do manual intervention if the resource absolutely can’t coexist.
        

---

✅ **Memory Hook** → Think **“Create before Kill”**.

- If both can exist → `create_before_destroy`.
    
- If not → blue/green or rename.
    
- If really blocked → import/state/taint.
    

---