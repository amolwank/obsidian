# 🧩 20 AWS Solutions Architect Scenario-Based Interview Q&A

---

### **1. Scenario:**

Your client wants to host a static website with high availability and low cost. What solution would you design?

**Answer:**  
Use **Amazon S3** for static website hosting, integrate with **CloudFront** for global low-latency delivery, and enable **Route 53** for DNS. Make the S3 bucket private and allow access only via CloudFront with **OAC** for security.

---

### **2. Scenario:**

You need to design a **highly available web application** across regions. How do you do it?

**Answer:**  
Deploy app servers in **multiple regions**, use **Route 53 latency-based routing** or **Global Accelerator**, store data in a **multi-region database (Aurora Global Database or DynamoDB Global Tables)**, and use **S3 cross-region replication** for static assets.

---

### **3. Scenario:**

How would you **secure an S3 bucket** containing sensitive data?

**Answer:**

- Keep bucket **private**
- Use **S3 Bucket Policies** with least privilege
- Enable **Server-Side Encryption (SSE-KMS)**
- Restrict access via **IAM roles**
- Enable **MFA Delete** and **CloudTrail logging**
    

---

### **4. Scenario:**

A customer’s website is experiencing **sudden traffic spikes**. How would you handle it?

**Answer:**  
Use an **Auto Scaling Group (ASG)** with EC2 behind an **Application Load Balancer (ALB)**. Add **CloudFront caching** for static content. Optionally, use **AWS WAF** for DDoS protection.

---

### **5. Scenario:**

Your company wants to **migrate a monolithic on-prem app to AWS**. How would you plan it?

**Answer:**
- Use **AWS Application Migration Service (MGN)** for lift-and-shift.
- Break down into **microservices** over time with **ECS/EKS**.
- Store data in **RDS or DynamoDB**.
- Use **CloudWatch + X-Ray** for monitoring during migration.

---

### **6. Scenario:**

How would you implement **disaster recovery (DR)** for a critical app in AWS?

**Answer:**

- Choose DR strategy: Backup & Restore, Pilot Light, Warm Standby, or Multi-site Active-Active.
- Example: Use **RDS Multi-AZ** or **Aurora Global Database**, replicate S3 buckets across regions, and use **Route 53 failover routing** for regional failover.
    

---

### **7. Scenario:**

How do you design a **secure VPC** for a 3-tier application?

**Answer:**

- **Public Subnets** → Load Balancers
- **Private Subnets** → App servers + DB servers
- **NAT Gateway** for outbound internet
- **Security Groups + NACLs** for layered security
- **VPC Flow Logs** for monitoring
    

---

### **8. Scenario:**

How would you design a **real-time analytics pipeline**?

**Answer:**

- Ingest data via **Kinesis Data Streams**
- Process with **Kinesis Data Analytics or Lambda**
- Store in **S3/Redshift**
- Query with **Athena/QuickSight**

---

### **9. Scenario:**

How do you implement **centralized IAM management** across multiple AWS accounts?

**Answer:**  
Use **AWS Organizations** + **Service Control Policies (SCPs)** for governance. Enable **AWS SSO (IAM Identity Center)** for centralized identity management.

---

### **10. Scenario:**

How would you design a **CI/CD pipeline** for deploying applications on AWS?

**Answer:**  
Use **CodeCommit/GitHub** → **CodeBuild** → **CodeDeploy or ECS/EKS**. Automate with **CodePipeline**. Add **manual approval stages** for production.

---

### **11. Scenario:**

How would you optimize costs for an EC2-heavy workload?
**Answer:**
- Use **Auto Scaling**
- Buy **Reserved Instances** or **Savings Plans**
- Use **Spot Instances** for non-critical workloads
- Right-size instances with **Compute Optimizer**
    

---

### **12. Scenario:**

How do you secure an **API hosted on AWS**?

**Answer:**
- Deploy API using **API Gateway**
- Authenticate with **Cognito / IAM auth / Lambda authorizer**
- Protect with **WAF** and **rate limiting**
- Enable **CloudWatch logs**
---

### **13. Scenario:**

How would you design an **IoT data ingestion system**?

**Answer:**  
Devices → **IoT Core** → stream into **Kinesis / SQS** → process with **Lambda** → store in **DynamoDB / S3** → visualize with **QuickSight**.

---

### **14. Scenario:**

You need **low-latency access to application data** across the globe. What do you use?

**Answer:**  
Use **DynamoDB Global Tables** for multi-region replication or **Aurora Global Database**. Add **CloudFront caching** for static assets.

---

### **15. Scenario:**

Your customer complains about **slow application performance**. How do you troubleshoot?

**Answer:**

- Check **CloudWatch metrics** (CPU, memory, latency)
- Use **X-Ray** for tracing bottlenecks
- Check **ALB logs** and **VPC Flow Logs**
- Scale resources or add **caching (ElastiCache/CloudFront)**
    

---

### **16. Scenario:**

How do you protect your app from **DDoS attacks**?

**Answer:**  
Use **AWS Shield (Standard/Advanced)** + **WAF** with rate-limiting rules + **CloudFront** for edge protection.

---

### **17. Scenario:**

How would you design a **multi-tenant SaaS application** in AWS?

**Answer:**

- Use **Cognito** for tenant authentication
    
- Use **separate DynamoDB partitions or RDS schemas** for tenant data isolation
    
- Deploy app on **EKS/ECS with namespaces**
    
- Add **CloudWatch dashboards per tenant**
    

---

### **18. Scenario:**

How would you build a **data lake in AWS**?

**Answer:**

- Store raw data in **S3 (Data Lake)**
- Use **Glue** for ETL + cataloging
- Query with **Athena**
- Visualize with **QuickSight**
- Secure with **Lake Formation**
    

---

### **19. Scenario:**

How would you migrate a database with **minimal downtime**?

**Answer:**  
Use **AWS DMS (Database Migration Service)** with **ongoing replication** until cutover. Combine with **RDS/Aurora** for managed service.

---

### **20. Scenario:**

How do you ensure compliance and governance across AWS accounts?

**Answer:**

- Use **AWS Config** + **Config Rules** for compliance checks
- **CloudTrail** for auditing
- **Organizations + SCPs** for policy enforcement
- **Security Hub + GuardDuty** for continuous monitoring
    

---
