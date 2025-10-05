# What I do (high level)

1. **Infra first**: create VPC, subnets, route tables, NATs, and security groups.
2. **Provision EKS control-plane** with Terraform (EKS resource or, better, `terraform-aws-modules/eks/aws` module).
3. **Provision worker compute**: managed node groups, self-managed nodes, or Fargate profiles.
4. **Bootstrap cluster add-ons** (CNI, CloudWatch, metrics, ingress, cert-manager, aws-load-balancer-controller).
5. **Enable IRSA** (create OIDC provider + IAM roles for ServiceAccounts).
6. **Connect tooling**: kubeconfig, Kubernetes provider or GitOps (ArgoCD) for app deployments.
7. **Operate**: autoscaling, monitoring, security (RBAC, PodSecurity, guardrails).

---
# Minimal, practical Terraform example (conceptual)

Use the official module for production-ready setup. This is a short example showing essentials.
```
terraform {
  required_version = ">= 1.4"
  backend "s3" {
    bucket = "org-terraform-state"
    key    = "eks/prod/cluster.tfstate"
    region = "us-east-1"
  }
}

provider "aws" {
  region = var.region
}

module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "4.x"
  name    = "eks-vpc"
  cidr    = var.vpc_cidr
  azs     = var.azs
  private_subnets = var.private_subnets
  public_subnets  = var.public_subnets
}

module "eks" {
  source  = "terraform-aws-modules/eks/aws"
  version = "20.x"

  cluster_name    = var.cluster_name
  cluster_version = "1.27"
  subnets         = module.vpc.private_subnets
  vpc_id          = module.vpc.vpc_id

  manage_aws_auth = true

  node_groups = {
    ng-ondemand = {
      desired_capacity = 2
      max_capacity     = 4
      min_capacity     = 1
      instance_types   = ["t3.medium"]
      subnet_ids       = module.vpc.private_subnets
    }
  }

  enable_irsa = true
}
```
**Notes:**
- `terraform-aws-modules/eks/aws` handles many details (IAM roles, OIDC, node group bootstrapping).    
- Use S3 backend + DynamoDB locking for state safety.
    
---
# Post-provision steps

- **kubeconfig** (locally):
- `aws eks update-kubeconfig --region $REGION --name $CLUSTER_NAME`
- or configure Kubernetes provider in Terraform using `aws_eks_cluster` outputs for automation.
- **Install add-ons** (examples): use Helm or the module’s `eks_addons`:
    - aws-load-balancer-controller
    - cert-manager
    - metrics-server / prometheus
    - cluster-autoscaler
- **Enable logging & monitoring**: CloudWatch Container Insights or Prometheus + Grafana.

---

# Best practices (must-mention in interview)

- **Use a module** (well-maintained EKS module) instead of hand-crafting all resources.
- **Separate state**: keep cluster infra, node groups, and app infra in different state scopes when needed.
- **IRSA** (OIDC provider + IAM roles per service account) — avoid static AWS keys in pods.
- **Managed node groups or Fargate** for lower ops; self-managed if you need custom AMIs or DaemonSets requiring node control.
- **Enable RBAC & PodSecurity / PSP replacement** for security posture.
- **Tagging & naming** consistent across modules for cost allocation.
- **Pin versions** (Terraform, providers, module) to avoid unpredicted changes on upgrades.
- **CI/CD**: run `terraform plan` on PRs and only allow `apply` from CI with restricted IAM.
- **Enable cluster control-plane logging** & enable encryption at rest for secrets if needed.

---

# Short interview answer (30–45s)

“I provision EKS by first creating VPC/networking, then use a well-supported Terraform module (or `aws_eks_cluster` + `aws_eks_node_group`) to create the control plane and worker nodes. I enable IRSA (OIDC) for pod IAM, bootstrap core add-ons (CNI, ingress, metrics) with Helm, and manage state in S3 with locking. Post-provision I wire up kubeconfig, install monitoring and autoscaling, and manage app deployments via GitOps so infrastructure changes are only applied through CI/CD.”