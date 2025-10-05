# High-level goals

- **Availability:** survive region failure with minimal downtime.
- **Isolation & governance:** each account boundaries for blast-radius, security.
- **Automated failover:** minimize manual steps for promotion.
- **Cost-effective:** balance active-active vs active-passive tradeoffs.
---

# Recommended architecture (summary)

- Use **AWS Organizations** with OUs: `Shared-services`, `Prod`, `Non-prod`, `DR`.
- In each **AWS account** (or account pair) run an **EKS cluster** in one or more regions.
    - Primary cluster in **Account A, Region 1**.
    - DR cluster in **Account B, Region 2** (active-passive) — or active-active if business requires lower RTO.
- **Centralized shared services** (logging, CI/CD, artifact registry) in a management account or replicated across regions.
- **Data replication**: application data replicated cross-region (database replication, S3 replication, cross-region caches or event replication).
- **Traffic failover** via DNS + health checks (Route53 failover) or Global Accelerator for faster failover and static IPs.
- **IaC & GitOps**: Terraform to provision infra + ArgoCD/Flux for app sync to clusters; pipelines in a centralized CI account.
- **Backups & snapshots** automated (Velero for K8s objects + PV snapshots / DB snapshots).
- **Security & policy**: SCPs, AWS Config rules, and guardrails; IRSA for pod AWS permissions.

---

# Detailed components & how they fit

1. **Account topology**
    - Use separate accounts for Prod and DR (prevents accidental cross-impact).
    - Shared services (CI/CD, pipeline runners, artifact repos, central log/monitor) live in a management account and are multi-region (or standby in DR region).   
2. **Cluster placement**
    - Provision **EKS cluster in primary region** (multi-AZ).  
    - Provision **EKS cluster in DR region** (multi-AZ) in separate account. Keep cluster configs (node groups, addons) identical via Terraform modules.    
3. **Infrastructure as Code**
    - Use **Terraform modules** to create identical clusters and networking across regions/accounts.    
    - Store remote state per account/region (S3 + locking).    
    - CI/CD (GitHub Actions / CodePipeline) handles `plan` and `apply` and promotes clusters via GitOps.    
4. **Application deployment & sync**
    - Use **GitOps (ArgoCD/Flux)** to continuously sync app manifests to both clusters.   
    - By default, DR cluster can stay synced but traffic routed to primary only (active-passive). For active-active, both get traffic.    
5. **Data replication**
    - **Stateless** services: keep image registry & config synced.   
    - **Object storage**: S3 cross-region replication (CRR).    
    - **Databases**: use global DB solutions (Aurora Global DB) or cross-region replication (read-replicas → promote secondary on failover).    
    - **Stateful K8s volumes**: use PV snapshot/replication (AWS EBS snapshots copied cross-region) or run stateful DB as a managed global DB.    
6. **Backups**
    - Use **Velero** for cluster resources + PV snapshots; back up to S3 in both regions.    
    - DB snapshots scheduled and copied cross-region.    
    - Test restore automation.    
7. **DNS & traffic failover**
    - Use **Route53** with health checks + failover routing (fast but DNS-based).    
    - For faster/global failover and static IPs, use **AWS Global Accelerator** fronting ALBs in each region. Global Accelerator can react faster and provide consistent anycast IPs.    
8. **Networking**
    - Use **Transit Gateway / VPC Peering** if you need inter-region connectivity between VPCs (for data sync or cross-account access).    
    - Keep DR networking ready (route tables, NACLs, subnet design) identical.    
9. **Security & Permissions**
    - **IRSA** (OIDC) per cluster to map service accounts to AWS roles.    
    - IAM least privilege; cross-account assume-role for CI pipelines.    
    - SCPs to prevent dangerous actions in prod accounts.    
10. **Observability & Ops**
    - Centralize logs/metrics: CloudWatch, Prometheus remote-write to central long-term storage, and tracing (X-Ray/Jaeger). Ensure logs/metrics are available in DR region or replicated.    
    - Health checks and runbooks: automated health monitors that trigger failover playbooks.    
11. **Testing & Runbooks**
    - Regular **DR drills** (automated) to validate failover, restore, and runbooks.    
    - Record RTO & RPO during drills and tune design accordingly.    

---

# DR modes & tradeoffs

- **Active-Passive (recommended for cost)**
    
    - DR cluster is warm or cold (kept synced but scaled down). Failover promoted manually/automatically.
        
    - Lower cost, higher RTO than active-active.
        
- **Active-Active (lower RTO, higher cost)**
    
    - Both clusters receive traffic (global LB), requires conflict-free data replication and stronger consistency controls. Harder for stateful apps.
        
- **Pilot Light**
    
    - Minimal infra in DR, larger parts spun up on failover. Shorter RPO, longer RTO.
        

---

# RTO / RPO considerations

- **Stateless** apps → RPO ~0 (images/config replicated), RTO minutes (DNS TTL, Global Accelerator).
    
- **Stateful** DB → RPO depends on replication tech (Aurora Global ~ seconds; cross-region read replica promotion minutes).
    
- Choose architecture based on business RTO/RPO.
    

---

# Implementation checklist (practical steps)

1. Design account OU structure and create accounts in AWS Organizations.
    
2. Build Terraform modules for VPC + EKS + node groups + IAM + OIDC (IRSA).
    
3. Provision primary EKS (account A, region 1) and DR EKS (account B, region 2).
    
4. Configure ECR/container registry replication or push images to both regions.
    
5. Setup GitOps (ArgoCD) with two targets — primary active, DR standby.
    
6. Implement DB replication (Aurora Global or cross-region read replicas + promotion scripts).
    
7. Implement S3 CRR for object data.
    
8. Configure backup (Velero) and test restore into DR.
    
9. Set up Route53 failover or Global Accelerator and health checks.
    
10. Centralize logging/metrics and replicate/forward to DR.
    
11. Automate failover runbooks and test via scheduled DR drills.
    
12. Add SCPs, Config rules, auditing, and guardrails.
    

---

# Example failover playbook (brief)

1. Detect region failure via health checks/monitoring.
    
2. Promote DR DB replica (or switch to Aurora secondary).
    
3. Promote DR cluster (scale up node groups if warm/cold).
    
4. Switch traffic: update Global Accelerator endpoint group weights or change Route53 failover.
    
5. Verify application health and traffic.
    
6. Execute post-failover validation and alert stakeholders.
    

---

# Cost & operational notes

- Active-active doubles infra cost; active-passive reduces it but needs careful warm-up procedures.
    
- Warm DR (scaled-down nodes, autoscale up on fail) offers compromise.
    
- Verify cross-region data transfer costs (S3 CRR, DB replication, snapshots).
    

---

# Quick interview-ready elevator pitch (30–45s)

> “I’d use a multi-account design with a primary EKS cluster in the primary account/region and a DR EKS cluster in a separate account/region. Infrastructure is provisioned with Terraform modules for parity; apps are synced via GitOps (ArgoCD). Data replication is handled by Aurora Global DB (or cross-region replicas) for state, and S3 cross-region replication for objects. Route53 failover or Global Accelerator handles traffic switching. Backups (Velero & snapshots) and regular DR drills ensure we meet RTO/RPO goals. This balances isolation, security, and automated failover while keeping costs manageable with a warm active-passive strategy.”