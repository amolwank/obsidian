## 📂 Types of Terraform Files

### 1. **Main Configuration Files (`*.tf`)**
- Written in **HCL (HashiCorp Configuration Language)**.
- Define the **infrastructure resources**, providers, variables, outputs, etc.
- Commonly split into logical files:
    - `main.tf` → core resources (e.g., EC2, VPC, RDS).
    - `provider.tf` → provider configs (AWS, GCP, etc.).
    - `variables.tf` → input variables.
    - `outputs.tf` → output values.
    - `locals.tf` → local values.
        
---

### 2. **Terraform State Files (`terraform.tfstate` / `terraform.tfstate.backup`)**

- Store the **current state** of infrastructure (resource IDs, metadata, dependencies).
- `terraform.tfstate.backup` is the backup of the last known state.
- Used by Terraform to determine what changes are needed.
- Should be **stored securely** (S3 + DynamoDB lock for teams).

---
### 3. **Variable Definition Files (`*.tfvars` or `terraform.tfvars`)**
- Contain values for input variables.
- Used to separate configuration from data (environment-specific).
- Example: `dev.tfvars`, `prod.tfvars`.

👉 Example `terraform.tfvars`:
```
instance_type = "t3.micro"
region        = "us-east-1"
```
### 4. **Provider Plugin Files**

- Downloaded automatically by Terraform (`.terraform/` directory).
- Contain the **binaries** needed to interact with cloud providers (AWS, Azure, GCP, etc.).
- Not manually edited.

---
### 5. **Lock File (`.terraform.lock.hcl`)**

- Records the **provider versions** used.
- Ensures consistent builds across environments.
- Should be committed to version control.

---
### 6. **Override Files (`override.tf`, `*.auto.tfvars`)**
- `override.tf` → overrides settings in other `.tf` files (not commonly used).
- `*.auto.tfvars` → automatically loaded variable definitions (no need to specify with `-var-file`).

---

### 7. **Module Files**

- When using modules, each module has its own `.tf` files (`main.tf`, `variables.tf`, `outputs.tf`).
- Helps in reusing infrastructure components (e.g., VPC module, EC2 module).

---
### 8. **JSON Config Files (`*.tf.json`)**
- Alternative to `.tf` — Terraform configs can also be written in JSON.
- Rare in practice, mostly used for automation.
---
## 📌 Quick Summary (Interview Style)
- **`.tf`** → main configuration files.
- **`terraform.tfstate`** → stores current infra state.
- **`terraform.tfstate.backup`** → last backup of state.
- **`.tfvars / terraform.tfvars`** → variable values.
- **`.terraform.lock.hcl`** → provider dependency lock.
- **`.auto.tfvars`** → auto-loaded variables.
- **`.terraform/`** → provider plugins & modules.
- **`.tf.json`** → JSON alternative to `.tf`.
