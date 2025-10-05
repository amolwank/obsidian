## 🔹 How to Integrate Terraform with GitHub Actions Safely

### 1. **Repository Setup**

- Store Terraform code in GitHub repo.
- Protect `main` branch with **PR reviews** and **required checks**.

---

### 2. **GitHub Actions Workflow**

Typical `terraform.yml` flow:

```
name: Terraform CI/CD

on:
  pull_request:
    branches: [ "main" ]   # Preview on PR
  push:
    branches: [ "main" ]   # Deploy on merge

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: ${{ secrets.AWS_ROLE }}
          aws-region: us-east-1

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3

      - name: Terraform Init
        run: terraform init

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      - name: Terraform Apply
        if: github.ref == 'refs/heads/main'
        run: terraform apply -auto-approve tfplan
```

### 3. **Safety Mechanisms**

- **Plan on PRs** → reviewers see infra changes before merging.
- **Manual approvals** → use `workflow_dispatch` or `environment protection rules` for prod.
- **Remote state** → S3 + DynamoDB (or Terraform Cloud) for safe collaboration.
- **IAM Roles** → Use OIDC + IRSA instead of long-lived AWS keys.
- **Secrets in GitHub** → DB passwords, AWS role ARNs stored in **GitHub Secrets**, not code.

---
### 4. **Environment Separation**
- Use **separate workflows** or **Terraform workspaces** for `dev`, `staging`, `prod`.
- Example:
    - Dev → auto-deploy on push  
    - Staging/Prod → require **manual approval**
        
---

### 5. **Rollback Strategy**
- Since Terraform code is versioned in Git, rollback = revert commit + re-run pipeline.
- Always pin module/provider versions.

---

## 🔹 Interview-Ready Answer (1 min)

_"I integrate Terraform with GitHub Actions by creating a pipeline that runs `terraform plan` on pull requests so reviewers can see proposed infra changes. On merge to main, the pipeline runs `terraform apply` using a remote state backend in S3 with DynamoDB locking. For security, I use OIDC-based IAM roles instead of static AWS keys, and store secrets in GitHub Secrets. I separate dev, staging, and prod deployments, with manual approvals for prod. This ensures deployments are consistent, auditable, and safe from accidental infra changes."_

