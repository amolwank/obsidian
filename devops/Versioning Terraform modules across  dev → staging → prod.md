## **Approach to Module Versioning**

### 1. **Source Control (Git) + Tags**

- Store modules in a **Git repo** (GitHub/GitLab/CodeCommit).
- Use **semantic versioning** (`v1.0.0`, `v1.1.0`, etc.) with tags.
- Environments point to **specific tags**, not `main`.

```
module "vpc" {
  source  = "git::https://github.com/org/terraform-modules.git//vpc?ref=v1.2.0"
  cidr    = var.cidr
}
```
### 2. **Terraform Registry (Private/Public)**

- Publish modules to a **private registry** (Terraform Cloud/Enterprise, or AWS CodeArtifact).
- Example:

```
module "eks" {
  source  = "app-team/eks/aws"
  version = "2.3.1"
}
```

### 3. **Environment Pinning**

- **Dev**: Uses latest (to test new features).
- **Staging**: Uses tested stable version.
- **Prod**: Uses “locked” version until validated.
- This ensures **progressive rollout** → dev → staging → prod.    

---
### 4. **Change Promotion Workflow**
- New version released → tested in **dev**.
- If stable → promoted to **staging**.
- After validation → rolled out to **prod**.
- Managed via **Git branching or pull requests**.    

---
### 5. **Tools for Better Management**
- **Dependabot/Renovate** → auto-update module versions with PRs.
- **Terragrunt** → can pin versions per environment and keep DRY configs.
- **CI/CD pipeline** → ensures version bumps go through testing.

---
## 🔹 **Interview-Ready Answer (45 sec)**

_"We manage module versioning using Git tags with semantic versioning. Each environment points to a specific module version — dev usually tracks the latest version for testing, staging uses a stable release, and prod is pinned to a validated version. This way, changes are promoted progressively through environments. We also use CI/CD pipelines to test modules and enforce version pinning, and tools like Dependabot help us manage updates. This ensures consistency, rollback safety, and controlled rollout of infrastructure changes across accounts."_
