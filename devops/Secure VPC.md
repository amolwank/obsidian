# High-level goals

- **Network isolation** between tiers (public vs private).
    
- **Least privilege** (access only where needed).
    
- **Defense-in-depth**: NSGs/NACLs + SGs + IAM + encryption.
    
- **Observability & auditing** for incident response.
    
- **High availability** across AZs.
    

---

# Architecture overview (multi-AZ)

- **VPC** spanning 3 AZs (for HA).
- Subnet layout per AZ:
    - Public subnets (ALB/Internet-facing NLB) — one per AZ.
    - Private app subnets (ECS/EKS/Lambda/NODEs) — one per AZ.    
    - Private database subnets (RDS/Aurora) — one per AZ (no internet). 
    - Isolated management subnet (optional) for bastion if needed. 
- **Internet Gateway (IGW)** attached to VPC for internet egress/ingress only via public subnets.
- **NAT Gateway(s)** in each AZ for outbound internet from private subnets (use 1 per AZ to avoid cross-AZ outage).
- **Route tables**
    - Public RT → IGW.   
    - Private RT → NAT Gateway (per AZ preferred).    
    - DB/Isolated RT → no NAT (or very strict egress via proxy).    

---

# Network connectivity & multi-VPC / hybrid

- **VPC Peering** or **AWS Transit Gateway** for multi-VPC connectivity (Transit Gateway for many VPCs).
- **VPN or Direct Connect** to on-prem (if required) terminating into a Transit Gateway or VGW.
- Use **Route Table propagation** carefully; avoid leaking CIDRs unintentionally.

---
# Private endpoints & reduced internet exposure
- **VPC Endpoints (Interface + Gateway)** for AWS services:
    - S3 Gateway Endpoint (private S3 access).
    - DynamoDB Gateway Endpoint (if used).
    - Interface Endpoints for Secrets Manager, Systems Manager, ECR, KMS, CloudWatch, STS, etc.    
- **AWS PrivateLink** for exposing internal services to other VPCs without public IPs.

---

# Load balancing & edge protection

- **Application Load Balancer (ALB)** in public subnets (TLS termination, WAF).
- **AWS WAF** + ALB to block OWASP common threats and rate limit.
- Use **ACM** to manage TLS certs (private or public).
- If TCP/UDP required, use **NLB** (can be internal or internet-facing).
    

---

# Security groups & NACLs (rules & examples)

- **Security Groups** (stateful) — primary access control:
    
    - ALB SG: allow inbound TCP 443/80 from 0.0.0.0/0 (HTTPS preferred) → outbound to app SG.
    - App SG: allow inbound from ALB SG on app ports (e.g., 8080). Allow outbound to DB SG on DB port.
    - DB SG: allow inbound only from App SG on DB port (e.g., 5432). No public inbound.
    - Bastion/SSM SG: locked to admin office IPs if bastion used.
- **NACLs** (stateless) — optional extra layer, keep simple (deny overly broad ephemeral ranges).
- **Example SG rule** (DB SG): inbound TCP 5432 from App_SG; no 0.0.0.0/0 inbound.
    

---

# Access & management

- **Avoid SSH bastions** where possible: prefer **AWS Systems Manager Session Manager** (SSM) + IAM for interactive access.
- If bastion required: place in public subnet, restrict source IPs, use MFA + temporary credentials.
- **IAM**:
    - Least-privilege IAM roles for EC2/ECS/EKS service roles.
    - Use IAM conditions + service control policies (SCPs) in AWS Organizations when required.
- **Secrets**: Secrets Manager / Parameter Store (with KMS CMKs). No secrets in code or user data.
- **KMS**: Customer-managed CMKs for encrypting EBS, RDS, S3, secrets — use key policies and grants carefully.
    
---

# Data protection & encryption

- **Encryption in transit**: TLS for all client<>ALB and service<>service comms (mTLS where needed).
- **Encryption at rest**: RDS/Aurora, EBS, S3, DynamoDB all encrypted with KMS keys.
- **Backups**: RDS automated snapshots, cross-region copy for critical data. Test restores.
    

---

# Observability, auditing & threat detection

- **VPC Flow Logs** to CloudWatch Logs or S3 for traffic auditing.
- **CloudTrail** for account-level API/audit logging (send to central logging account).
- **GuardDuty** for threat detection.
- **Config** for resource compliance drift detection.
- **CloudWatch / Prometheus + Grafana** for metrics and alarms.
- **AWS X-Ray / OpenTelemetry** for distributed tracing.
- Centralize logs in an OpenSearch/CloudWatch Logs account with retention policies.

---

# Resilience & availability

- Multi-AZ deployment of compute and DB (Aurora multi-AZ or RDS Multi-AZ).
- NAT Gateway per AZ; avoid single point of failure.
- Health checks on ALB, auto-scaling groups across AZs.
- Use read replicas for scaling reads and cross-region replicas for DR if needed.

---

# CI/CD & infrastructure security

- **IaC**: Terraform / CloudFormation / CDK for reproducible infra. Store state securely (S3 with encryption + DynamoDB lock).
- **CI/CD**: least privilege deploy role, sign artifacts, use artifact repositories (ECR, S3).
- Run security checks in pipeline (static code analysis, container scanning, IaC linting).
- Automated test for infra: security groups, open ports, misconfigurations.

---

# Example CIDR & minimal diagram (quick)

- VPC CIDR: `10.0.0.0/16`
    
    - AZ-a public: `10.0.1.0/24` (ALB, NAT GW EIP)
        
    - AZ-a private app: `10.0.11.0/24`
        
    - AZ-a db: `10.0.21.0/24`
        
    - Repeat pattern for AZ-b and AZ-c (10.0.2x/24, 10.0.1x/24 etc)
        
- Keep room for future peering and transit — avoid overly small VPC ranges.
    

---

# Quick security rule examples (concise)

- ALB SG inbound: `TCP 443` from `0.0.0.0/0` → outbound to App_SG.
    
- App_SG inbound: from `ALB_SG` on `TCP 8080` → outbound to `DB_SG:5432`.
    
- DB_SG inbound: from `App_SG` on `TCP 5432` only.
    
- Management SG inbound: `TCP 22` or SSM port only from office IPs (prefer SSM agent, block SSH).
    

---

# Operational checklist (must do)

- Enable CloudTrail + VPC Flow Logs + GuardDuty.
- Enforce IAM password policies / MFA.
- Rotate KMS keys and secrets periodically.
- Pen-test / run vulnerability scans and remediate.
- Test DR and restore procedures every quarter.
- Least-privilege review for IAM roles monthly.

---

# Best practices / gotchas

- Prefer **SSM Session Manager** over open SSH.
- Use **VPC endpoints** to avoid egress to internet for AWS API calls.
- Don’t forget **DNS** (Route53 private hosted zones) for internal service discovery.
- Limit CIDR overlap when planning multi-VPC or on-prem connectivity.
- Monitor NAT Gateway and data transfer costs (can be expensive).