# 🚀 **AWS Cheat Sheet**

---

## **1. Core Concepts**

- **Region** → Geographical area (e.g., us-east-1).
- **Availability Zone (AZ)** → Physically isolated datacenters within a region.
- **Edge Locations** → Used by CloudFront & Route 53 for caching and DNS.

---
## **2. Compute**

- **EC2** → Virtual servers in the cloud.
    
    - Pricing: On-Demand, Reserved, Spot, Savings Plans.
        
- **Auto Scaling** → Scale EC2 instances based on demand.
    
- **Elastic Load Balancer (ELB)** → Distributes traffic across instances.
    
- **Lambda** → Serverless compute, pay per execution.
    
- **ECS / EKS** → Container orchestration (ECS = AWS-managed, EKS = Kubernetes).
    
- **Elastic Beanstalk** → PaaS for deploying applications.
    

---

## **3. Storage**

- **S3** → Object storage.
    
    - Storage classes: Standard, IA, Glacier, Intelligent-Tiering.
        
    - Features: Versioning, Lifecycle rules, Cross-region replication.
        
- **EBS** → Block storage for EC2.
    
- **EFS** → Shared file storage (POSIX).
    
- **FSx** → Managed Windows file server/Lustre.
    
- **Storage Gateway** → Hybrid cloud storage.
    

---

## **4. Databases**

- **RDS** → Managed relational DB (MySQL, PostgreSQL, Oracle, SQL Server).
    
- **Aurora** → AWS-native relational DB (MySQL/Postgres compatible, highly scalable).
    
- **DynamoDB** → NoSQL key-value store, serverless.
    
- **ElastiCache** → Managed Redis/Memcached.
    
- **Redshift** → Data warehouse.
    
- **Neptune** → Graph database.
    
- **DocumentDB** → MongoDB-compatible DB.
    

---

## **5. Networking**

- **VPC** → Isolated network environment.
    
- **Subnets** → Public/private subdivisions of a VPC.
    
- **Internet Gateway (IGW)** → Connects VPC to the internet.
    
- **NAT Gateway** → Private subnet to internet (outbound).
    
- **Route 53** → DNS & domain management.
    
- **Transit Gateway** → Connects multiple VPCs & on-prem.
    
- **Direct Connect** → Private dedicated connection to AWS.
    
- **Global Accelerator** → Improves global application performance.
    

---

## **6. Security & IAM**

- **IAM Users, Groups, Roles, Policies** → Access management.
    
- **IAM Identity Center (SSO)** → Centralized user access.
    
- **KMS** → Key Management Service (encryption).
    
- **SSM Parameter Store** → Secure config storage.
    
- **Secrets Manager** → Manage & rotate secrets.
    
- **Shield** → DDoS protection.
    
- **WAF** → Web Application Firewall.
    
- **CloudHSM** → Hardware security module.
    

---

## **7. Monitoring & Logging**

- **CloudWatch** → Metrics, logs, alarms, dashboards.
    
- **CloudTrail** → API activity logging.
    
- **Config** → Resource compliance tracking.
    
- **X-Ray** → Distributed tracing for apps.
    

---

## **8. Analytics & Big Data**

- **Athena** → Query S3 data with SQL.
    
- **Glue** → Serverless ETL.
    
- **Kinesis** → Real-time streaming.
    
- **EMR** → Managed Hadoop/Spark cluster.
    
- **QuickSight** → Business intelligence dashboards.
    

---

## **9. DevOps & Management**

- **CloudFormation** → Infrastructure as Code (YAML/JSON).
    
- **Terraform** (not AWS-native, but widely used).
    
- **CodeCommit** → Git repository.
    
- **CodeBuild** → CI build service.
    
- **CodeDeploy** → Automated deployment.
    
- **CodePipeline** → CI/CD orchestration.
    
- **Systems Manager (SSM)** → Manage EC2, patching, run commands.
    
- **Control Tower** → Multi-account governance.
    
- **Organizations** → Manage multiple AWS accounts.
    

---

## **10. Machine Learning & AI**

- **SageMaker** → Build, train, deploy ML models.
    
- **Rekognition** → Image & video analysis.
    
- **Comprehend** → Natural language processing.
    
- **Polly** → Text-to-speech.
    
- **Lex** → Chatbots (used in Alexa).
    
- **Transcribe** → Speech-to-text.
    
- **Translate** → Language translation.
    

---

## **11. Migration & Hybrid**

- **Snowball / Snowmobile** → Data transfer appliances.
    
- **DataSync** → Online data transfer.
    
- **Migration Hub** → Track migrations.
    
- **Outposts** → AWS services on-prem.
    

---

## **12. Cost Management**

- **Cost Explorer** → Analyze spend.
    
- **Budgets** → Set cost & usage alerts.
    
- **Trusted Advisor** → Best practice recommendations.
    
- **Savings Plans / Reserved Instances** → Cost optimization.
    

---

✅ **Quick Tip for Interview**  
If asked: _"How do you keep AWS environments secure and cost-effective?"_  
You can answer:

- Use **IAM roles & policies**, **KMS encryption**, **CloudTrail auditing**, and **Config rules** for security.
    
- Use **S3 lifecycle policies**, **EC2 Auto Scaling**, and **Savings Plans** for cost optimization.