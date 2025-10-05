In Terraform, a workspace is like a separate environment that has its own state file, allowing you to manage multiple sets of infrastructure from the same configuration
### Key Points
- Purpose->Manage different environments
- Default ->Terraform starts with one workspace named default.
- State Separation->Each workspace keeps its own terraform.tfstate file.
- Same code, Different State->You can reuse the same .tf files for multiple environments.
### Commands
```
terraform workspace list         -> List all workspaces
terraform workspace new dev
terraform workspace select dev
terraform workspace show
terraform workspace delete dev
```

#### Why Workspace Are Not Always Recommended in Production
- Hidden Complexity-> Hide the state in the backend
- State file coupling-> all workspaces in the same backend share the same configuration repo.
- Limited isolation->Workspaces don't give strict separation
- Secret Management challenges

#### Standard Recommended Production Approach:
Use separate folders/repo/ state files for each environment instead of workspaces.

```
terraform/
├── dev/
│   ├── main.tf
│   ├── variables.tf
│   ├── terraform.tfvars
│   └── backend.tf
├── staging/
│   ├── main.tf
│   ├── variables.tf
│   ├── terraform.tfvars
│   └── backend.tf
└── prod/
    ├── main.tf
    ├── variables.tf
    ├── terraform.tfvars
    └── backend.tf
```
