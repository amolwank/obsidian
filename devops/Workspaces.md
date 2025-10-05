## 🎯 What are Terraform Workspaces?

- Workspaces in Terraform allow you to **use the same code** to manage **multiple environments** (like dev, test, prod) without duplicating `.tf` files.
- Each workspace has its **own state file**.
    

---

## 🛠️ Why do we need them?

- **Separation of environments** → Avoid mixing dev/prod resources.
- **Reusability** → Write infrastructure code once, just change workspace.
- **Safe testing** → Try new changes in `dev` workspace without affecting `prod`.
    
---
## 🔑 Important Commands
```
terraform workspace list       # See all workspaces
terraform workspace new dev    # Create a new workspace
terraform workspace select dev # Switch to dev workspace
terraform workspace show       # Show current workspace

```

## 📖 Simple Analogy

Think of **workspaces like different project folders**, but sharing the same code:

- In **dev workspace** → S3 bucket might be `myapp-dev`.
- In **prod workspace** → S3 bucket might be `myapp-prod`.
    
Same Terraform config, but **different states & resources**.

---

## 📝 Easy line to remember

**“Terraform workspaces let us manage multiple environments (dev/test/prod) using the same code but with separate state files.”**