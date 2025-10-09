# 🚀 AWS Senior-Level Interview Cheat Sheet

---

## 1. **Networking & VPC**

- **VPC Design:**
    
    - Multi-AZ subnets (public, private app, private DB).
        
    - NAT Gateway per AZ, VPC Endpoints (S3, DynamoDB, Secrets Manager).
        
    - Transit Gateway for multi-VPC, multi-region routing.
        
- **Best practices:**
    
    - Private subnets for compute & DB.
    - Flow Logs for auditing.
    - SSM Session Manager instead of SSH.
        

**Q:** How do you design a secure multi-tier VPC?  
👉 Public ALB → App in private subnets → DB in isolated subnets, all encrypted, least-privilege SGs, NAT for outbound, VPC endpoints for AWS services.

---

## 2. **Compute & Containers**

- **ECS vs EKS vs Lambda**
    
    - **ECS**: Simple container orchestration (Fargate = serverless).
        
    - **EKS**: Kubernetes, portable, microservices-heavy workloads.
        
    - **Lambda**: Event-driven, short-running, no servers.
        
- **Scaling:** Auto Scaling Groups, HPA in EKS, Lambda concurrency.
    
- **Deployment:** Blue/Green, Canary, ArgoCD for GitOps in Kubernetes.
    

**Q:** Why choose EKS over ECS?  
👉 Standardized Kubernetes, multi-cloud portability, ecosystem (Ingress, Service Mesh, etc.).

---

## 3. **Storage & Databases**

- **S3:** Versioning, lifecycle, cross-region replication (CRR).
    
- **Aurora Global DB:** Low-latency reads, fast DR failover (<1 min).
    
- **DynamoDB Global Tables:** Multi-region active-active.
    
- **Caching:** ElastiCache (Redis), DynamoDB DAX.
    

**Q:** How do you design multi-region data replication?  
👉 Aurora Global DB or DynamoDB Global Tables, plus S3 CRR. Pick based on consistency vs latency needs.

---

## 4. **Security**

- **IAM:** Least privilege, SCPs in Organizations, IAM Roles not users.
    
- **KMS:** Encrypt EBS, RDS, S3.
    
- **Secrets:** Use Secrets Manager, rotate keys.
    
- **Network Security:** WAF + Shield + SGs + NACLs.
    
- **Detection:** GuardDuty, Config, CloudTrail, Inspector.
    

**Q:** How do you secure a VPC?  
👉 Segregated subnets, SGs with least privilege, VPC endpoints, NAT, WAF, encryption, SSM for access.

---

## 5. **High Availability & DR**

- **Multi-AZ:** Default for RDS, ALB, ASG.
    
- **Multi-region:** Global Accelerator + Route 53 health checks.
    
- **RTO/RPO:** Define upfront. Aurora Global DB or DynamoDB Global Tables for low RTO/RPO.
    

**Q:** How do you design an active-passive DR?  
👉 Primary in us-east-1, standby in us-west-2, Global Accelerator for failover, cross-region S3, Aurora Replica. Promote DB + reroute traffic.

---

## 6. **Monitoring & Observability**

- **Metrics:** CloudWatch + Prometheus/Grafana.
    
- **Logs:** Centralized logging (CloudWatch Logs, OpenSearch).
    
- **Tracing:** X-Ray, OpenTelemetry.
    
- **Alerts:** CloudWatch alarms → SNS/PagerDuty.
    

**Q:** How do you monitor microservices?  
👉 Use CloudWatch/Prometheus for metrics, X-Ray/OpenTelemetry for tracing, central log aggregation.

---

## 7. **CI/CD & IaC**

- **IaC:** Terraform / CloudFormation / CDK.
    
- **Pipelines:** GitHub Actions, CodePipeline, ArgoCD (for GitOps).
    
- **Best practices:** Infrastructure as Code + policy as code (OPA, Sentinel).
    

**Q:** How do you structure Terraform for multi-env?  
👉 Use root modules for environments (dev/stage/prod), reuse child modules, store remote state in S3+DynamoDB lock.

---

## 8. **Data & Analytics**

- **Athena + Glue:** Serverless querying and ETL.
    
- **Redshift:** Data warehouse, Spectrum for S3 queries.
    
- **Kinesis/MSK:** Real-time streaming.
    
- **EMR:** Big data batch.
    

**Q:** How do you design a data lake on AWS?  
👉 S3 (raw + curated), Glue catalog, Athena for queries, Redshift Spectrum for warehouse integration, Lake Formation for governance.

---

## 9. **Global Networking**

- **Global Accelerator:** Static anycast IPs, routes via AWS backbone.
    
- **Route 53:** DNS-based routing (geo, latency, failover).
    
- **CloudFront:** CDN for caching and edge security.
    

**Q:** When use Global Accelerator vs Route 53?  
👉 Global Accelerator = static IP, performance routing over AWS backbone. Route 53 = DNS-level failover, no static IP.

---

## 10. **Cost Optimization**

- Right-size instances, Reserved/Spot.
    
- S3 lifecycle to Glacier/IA.
    
- Lambda for infrequent workloads.
    
- Use Compute Savings Plans.
    
- Trusted Advisor, Cost Explorer, Budgets.
    

**Q:** How do you optimize AWS costs?  
👉 Use right-size + spot for compute, lifecycle policies for S3, reserved instances for DB, consolidate accounts with AWS Organizations.

---

## 11. **FinOps / Governance**

- **Organizations + SCPs.**
    
- **AWS Config** for compliance.
    
- **CloudTrail + GuardDuty** for auditing.
    
- **Budgets & Cost Anomaly Detection** for finance.
    

---

## 🔑 Interview Strategy

- Always **start with requirements** (HA, DR, security, compliance, budget).
    
- Break down into **network, compute, storage, security, monitoring**.
    
- Use **AWS Well-Architected Framework** (5 pillars: Operational Excellence, Security, Reliability, Performance, Cost Optimization).
    

---

⚡ **Pro tip:** For each AWS service, know:

- **What it is**
    
- **When to use**
    
- **One limitation**
    
- **One real-world use case**