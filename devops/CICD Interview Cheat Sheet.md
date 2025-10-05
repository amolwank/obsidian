# 🚀 CI/CD Interview Cheat Sheet (Senior-Level)

---

## 1. **Core Concepts**

- **CI (Continuous Integration)** → Developers integrate code frequently, automated build + test.
    
- **CD (Continuous Delivery/Deployment)** → Automated release pipeline.
    
    - _Delivery_: Manual approval before prod.
        
    - _Deployment_: Fully automated to prod.
        

---

## 2. **Pipeline Stages**

1. **Source** → Trigger on commit/merge (GitHub, GitLab, Bitbucket).
    
2. **Build** → Compile, package, containerize (Maven, Gradle, Docker).
    
3. **Test** → Unit, integration, security scans.
    
4. **Artifact Mgmt** → Push to registry (ECR, Nexus, Artifactory).
    
5. **Deploy** → Staging → Prod (Kubernetes, ECS, Lambda).
    
6. **Monitor** → Logs, alerts, rollback automation.
    

---

## 3. **Best Practices**

- **Shift Left Testing** → Run tests early.
    
- **Immutable Artifacts** → Same build → all environments.
    
- **Infrastructure as Code** → Terraform/CloudFormation integrated.
    
- **Secrets Mgmt** → Vault, SSM, Secrets Manager, not hardcoded.
    
- **Security in Pipeline** → SAST, DAST, dependency scanning.
    
- **Blue/Green or Canary** → Safer deployments.
    

---

## 4. **Popular CI/CD Tools**

- **CI:** Jenkins, GitHub Actions, GitLab CI, CircleCI.
    
- **CD:** ArgoCD, Spinnaker, Flux, Tekton.
    
- **Artifact:** Docker Hub, AWS ECR, Nexus.
    
- **Monitoring:** Prometheus, Grafana, ELK, Datadog.
    

---

## 5. **Key AWS CI/CD Services**

- **CodeCommit** → Git repo.
    
- **CodeBuild** → Build & test.
    
- **CodeDeploy** → Deploy apps.
    
- **CodePipeline** → Orchestrates CI/CD.
    
- **CodeArtifact** → Package mgmt.
    

---

## 6. **Deployment Strategies**

- **Rolling Update** → Gradual pod replacement.
    
- **Blue/Green** → Two environments, switch traffic.
    
- **Canary** → Small % of users first.
    
- **A/B Testing** → Split traffic by features.
    

---

## 7. **Common Interview Questions**

**Q1:** How do you ensure zero downtime deployment?  
👉 Use Blue/Green or Canary strategy with health checks and automated rollback.

**Q2:** How do you secure a CI/CD pipeline?  
👉 Restrict credentials, use IAM roles, secrets manager, enforce code scans, sign artifacts.

**Q3:** How do you roll back a bad deployment?  
👉 Use automated rollback in CodeDeploy/K8s, keep previous stable artifacts, maintain versioned Helm charts.

**Q4:** How do you scale CI/CD for microservices?  
👉 Use pipeline templates, parallel builds, dynamic agents, GitOps with ArgoCD.

**Q5:** Difference between Continuous Delivery vs Deployment?  
👉 Delivery requires manual approval before prod, Deployment is fully automated.

---

## 8. **Quick Commands / YAML (GitHub Actions Example)**

```
name: CI Pipeline
on:
  push:
    branches: [ "main" ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Build Docker Image
        run: docker build -t myapp:${{ github.sha }} .
      - name: Push to ECR
        run: |
          aws ecr get-login-password --region us-east-1 | docker login ...
          docker push <acct>.dkr.ecr.us-east-1.amazonaws.com/myapp:${{ github.sha }}

```

---

## 9. **Metrics to Track**

- **MTTR (Mean Time to Recovery)**.
    
- **Deployment Frequency**.
    
- **Lead Time for Changes**.
    
- **Change Failure Rate**.
    

_(DORA Metrics — industry standard for DevOps success)_

---

⚡ **Golden Rule:** CI/CD pipelines should be **fast, secure, and automated** — with rollback, testing, and monitoring baked in.

---