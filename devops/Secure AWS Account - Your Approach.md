
---

### ✅ **Answer: How I Secure My AWS Account — My Approach**

> My approach to securing an AWS account follows a **defense-in-depth** strategy — securing at multiple layers: identity, network, data, and monitoring.

---

#### **1. Identity & Access Management (IAM)**

- Enforced **least privilege access** using IAM policies and roles.    
- Used **IAM Identity Center (AWS SSO)** for centralized access control and MFA enforcement.
- Disabled use of the **root account** for daily tasks and protected it with **MFA**.
- Applied **service control policies (SCPs)** under AWS Organizations to restrict actions across accounts.
- Rotated access keys and used **temporary credentials via roles** instead of long-term keys.
    
---
#### **2. Network Security**

- Designed **VPCs with private and public subnets** following best practices.
- Used **Security Groups** for instance-level security and **Network ACLs** for subnet-level protection.
- Enabled **VPC Flow Logs** to monitor network traffic.
- Used **AWS WAF** and **Shield** to protect against web attacks (e.g., DDoS, SQL injection).
- Controlled connectivity with **VPN/Direct Connect** and private endpoints using **VPC Endpoint Services**.

---
#### **3. Data Security**
- Enabled **encryption at rest** (KMS-managed keys for S3, RDS, EBS, etc.).
- Enforced **encryption in transit** using HTTPS/TLS.
- Restricted S3 bucket public access and used **bucket policies** with **least privilege**.
- Implemented **S3 Object Lock** and versioning to prevent accidental or malicious deletion.

---
#### **4. Monitoring & Auditing**
- Enabled **AWS CloudTrail** in all regions to log all API calls.
- Used **AWS Config** for continuous compliance and drift detection.
- Enabled **AWS GuardDuty**, **Security Hub**, and **Inspector** for threat detection and vulnerability scanning.
- Set up **CloudWatch alarms** and **SNS notifications** for critical events.

---
#### **5. Compliance & Governance**
- Implemented **multi-account setup using AWS Control Tower** with baseline guardrails.
- Used **Service Catalog and Tag Policies** for resource governance.
- Regularly reviewed findings in **AWS Security Hub** to ensure alignment with standards like CIS, SOC 2, and HIPAA.
    
---

✅ **Summary line for interviews:**

> “In short, I secure AWS accounts through layered controls — strong identity management, network isolation, data encryption, continuous monitoring, and governance — following AWS Well-Architected and CIS benchmark best practices.”