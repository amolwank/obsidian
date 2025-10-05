*"Yes, I have implemented GitHub Actions in my projects to automate end-to-end CI/CD pipelines for both infrastructure and application deployments.

For **infrastructure**, I set up a dedicated GitHub Actions workflow triggered on `push` or `pull_request` to the main branch. The workflow included steps to check out the code, configure AWS credentials securely using GitHub Secrets, and run Terraform commands: `terraform init`, `terraform plan`, and `terraform apply`. We used a **remote S3 backend with native state locking** to ensure consistency across environments, and separate workspaces for **dev, staging, and production**. I also included **linting and unit tests** for Terraform modules to catch errors early.

For the **application layer**, another workflow built, tested, and packaged Docker images on every push. Images were pushed to **Amazon ECR** following a structured tagging strategy (`branch-name` or `version` tags). Deployment to Kubernetes was automated using **kubectl and Helm charts**. We maintained separate namespaces for dev/staging/prod clusters and implemented **blue/green deployments** for minimal downtime. Rollbacks could be triggered automatically if Helm detected deployment failures.

To optimize efficiency, the workflows leveraged **parallel jobs**, **caching of dependencies**, and secure management of secrets. Logs and failure notifications were configured via GitHub Actions and integrated with **Slack**, ensuring rapid feedback.

Overall, this CI/CD setup allowed fully automated infrastructure provisioning and application deployment, improved consistency across environments, reduced manual errors, and scaled seamlessly with traffic. We kept costs minimal by using **serverless runners, caching Docker layers, and pay-per-use AWS services**."*

Example: `.github/workflows/terraform-tests.yml`

```
name: Terraform CI

on:
  pull_request:
    branches: ["main"]
  push:
    branches: ["main"]

jobs:
  terraform:
    name: Terraform Checks
    runs-on: ubuntu-latest

    steps:
      # Checkout repository
      - name: Checkout code
        uses: actions/checkout@v4

      # Setup Terraform
      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: 1.8.5   # choose your version

      # Format check
      - name: Terraform Format
        run: terraform fmt -check -recursive

      # Init
      - name: Terraform Init
        run: terraform init -backend=false

      # Validate syntax
      - name: Terraform Validate
        run: terraform validate -no-color

      # TFLint
      - name: Run TFLint
        uses: terraform-linters/setup-tflint@v4
      - run: tflint --recursive

      # Security scan with Checkov
      - name: Run Checkov
        uses: bridgecrewio/checkov-action@v12
        with:
          directory: .

      # Generate Terraform Plan (but don’t apply)
      - name: Terraform Plan
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: terraform plan -no-color -out=tfplan

      # (Optional) Upload Plan Artifact
      - name: Upload Plan
        uses: actions/upload-artifact@v4
        with:
          name: terraform-plan
          path: tfplan

```