##### Introduction
Terraform is an open-source Infrastructure as Code (IaC) tool created by HashiCorp that lets you define, provision, and manage infrastructure in a declarative way.

##### Core Components
- [[Providers]] (AWS, Azure, GCP, Kubernetes)
- [[Resources]] and [[Data sources]]
- [[Variables]]
- [[Output]]
- Locals (DRY code)

##### State Management
- [[Purpose of terraform.tfstate]]
- Local vs remote state.
- [[State locking]] (S3+DynamoDB in aws)
- terraform state commands
- [[State drift & terraform refresh]]
##### [[Modules]]
##### Meta-Arguments
- depends_on (explicit dependency) ->Terraform **auto-manages dependencies** via references, but `depends_on` is for **manual override**.
- [[count vs for_each]]
- [[lifecycle arguments ]](prevent_destroy,create_before_destroy, ignore-changes).

##### Functions
- String functions (upper, lower, replace)
- Collection functions (lenght, join, split)
- File functions(file, filebase64)
- Numeric & date/time functions
##### [[Workspaces]] & Environments
 - Default and custom workspaces.
 - When to use workspaces vs separate state files.

##### Backends
 - Purpose of backends
 - S3 backend + DynamoDB locking (AWS)
 - Terraform Cloud backend.
 - Remote execution vs local execution.
##### [[Proviosioners]]
- local-exec and remote-exec
- When to avoid provisioners & use alternatives.
##### Advance Usage
- [[terraform import ]]-> managing existing infra.
- [[terraform taint & terraform untaint]]
- terraform graph (dependency visualization)
- terraform apply -target (targeted apply)

##### Key Points
- Purpose: Automates creation, update, and deletion of infrastructure across multiple platforms like AWS, Azure, GCP, and even on-premises systems.
- Language: Uses HCL(HashiCorp Configuration Language), which is human-readable.
- Cloud-agnostic: Works with many provides, not tied to one.
- Declarative: You write what you want, Terraform figures out how to get there. 

[[Terraform Workflow]]
Single component [[destroy]]?

[[Dynamic Blocks in Terraform]]

Tags: #Terraform
Ref: [[Workspace]]

## 🔹 **Terraform Scenario-Based Interview Questions**

### **State Management**
1. You have multiple teams working on the same AWS account. How would you manage Terraform state to avoid conflicts? -[[Multiple teams, same AWS account]]
2. What happens if your Terraform state file gets corrupted or deleted? How would you recover it? -[[Terraform state file is corrupted or deleted]]
3. How do you manage state when deploying the same infra in multiple regions or accounts? - [[Same infrastructure across multiple regions or AWS Account]] 
4. How would you handle importing existing AWS resources into Terraform state without downtime?- [[Importing existing AWS resource into terraform]]
---
### **Modules & Reusability**
5. [[How would you design Terraform modules for an organization with 50+ AWS accounts]]? 
6. How do you manage versioning of modules across different environments (dev, staging, prod)? - [[Versioning Terraform modules across  dev → staging → prod]]
7. If a module update breaks infra in production, how would you roll back? - [[Roll Back a Broken Module Update]]
---
### **CI/CD & Collaboration**
8. How would you integrate Terraform with GitHub Actions for safe deployments? - [[Integrate Terraform With GitHub Actions]]
9. How do you ensure that developers don’t run `terraform apply` directly from their laptops?  - [[Prevent cowboy changes in infra]]
10. How do you handle Terraform plan reviews in pull requests? - [[Terraform Plan reviews]]

---
### **Security & Compliance**
11. How would you manage secrets (like DB passwords) in Terraform securely? - [[Manage Secrets Securely in Terraform]]
12. How do you enforce compliance rules, e.g., ensuring S3 buckets are always encrypted, across all Terraform codebases?  - [[Enforce compliance rules]]
13. How would you prevent accidental deletion of critical resources like RDS or S3 buckets? - [[Prevent accidental deletion of critical resources]]
---
### **Scaling & Large Infrastructure**
14. How would you structure Terraform for a large project with hundreds of resources? One state file or multiple? Why? - [[Terraform for large project]]
15. How do you manage Terraform deployments in a multi-region, multi-account AWS setup? - [[Managing Multi-region, multi-account AWS Setup]]
16. What’s your approach to performance issues when `terraform plan` takes too long due to a huge state file? - [[Huge State File]]
    

---

### **Real-World Troubleshooting**
17. You ran `terraform apply`, and it’s stuck or failed halfway — how do you fix the drift without downtime?    -[[terraform apply failed or stuck halfway]]
18. A developer accidentally removed a resource from Terraform code but not from AWS — what happens during the next `terraform apply`? - [[Accidentally removed a resource]]
19. How do you handle situations where a resource can’t be created before another is destroyed?  - [[Handle situations where a resource can’t be created before another  ]]
20. How would you debug a Terraform plan where resources are being replaced unexpectedly? - [[Debug Terraform resource being replaced]]
---
### **Multi-Cloud & Advanced Use Cases**
21. How would you use Terraform to manage resources across AWS and Azure together? - [[Terraform Manages AWS + Azure Together]]
22. Can you explain how you would provision Kubernetes clusters with Terraform and manage them afterward? - [[Provision Kubernetes cluster with Terraform]]
23. If your organization uses Terraform Cloud/Enterprise, how do you enforce policies and manage team access?    
---
✅ **Pro Tip for Interviews:**  
When answering, don’t just give the **concept** — give a **mini real-world story**:

> _“In my last project, we had 50 AWS accounts. To manage state, I used S3 with DynamoDB locking per account, and split infra into environment-specific state files. We also used GitHub Actions so no one could directly run Terraform locally — all changes went through PR reviews with `terraform plan` shown as a comment.”_

