
### **Use this one:**
My name is Amol Wankhede, and I have over 16 years of experience in the IT industry. I started my career as a Java developer and later transitioned to cloud technologies. Over the years, I have primarily worked on AWS, focusing on infrastructure creation using Terraform.

I have experience managing microservices using Kubernetes and setting up CI/CD pipelines using GitOps approaches. Currently, I am working as a Cloud Architect, designing scalable, secure, and highly available 3-tier applications.

In my recent projects, I have designed custom data lakes using S3, along with services like Athena, Glue, and OpenSearch. I have also designed disaster recovery solutions for legacy applications to ensure business continuity.

Introduction in point:
- My name is **Amol Wankhede**, and I have **over 16 years of experience** in the IT industry.
- I began my career as a **Java Developer** and gradually transitioned into cloud technologies.
- Over the years, I have gained strong expertise in **AWS Cloud**, focusing on **infrastructure automation** using **Terraform**.
- I have hands-on experience in **managing microservices** with **Kubernetes** and implementing **CI/CD pipelines** following **GitOps principles** using tools like **ArgoCD** and **GitHub Actions**.
- Currently, I am working as a **Cloud Architect**, responsible for designing **scalable**, **secure**, and **highly available 3-tier applications** on AWS.
- In my recent projects, I have:
    - Designed a **custom data lake** using **Amazon S3**, integrated with **AWS Glue**, **Athena**, and **OpenSearch** for analytics.
    - Implemented **disaster recovery solutions** for **legacy applications** to ensure **high availability** and **business continuity**.
- My core strengths include **cloud architecture design**, **automation**, **DevOps integration**, and **cost-optimized cloud solutions**.
- I’m passionate about **building reliable cloud systems** and continuously improving **efficiency and resilience** in modern cloud environments.
---
#### Ideal for real interview delivery 👇

**“Hi, I’m Amol Wankhede. I have around sixteen years of experience in the IT industry. I actually started my career as a Java developer, but over time I developed a strong interest in cloud technologies, especially AWS.**

**For the past several years, I’ve been focusing on cloud infrastructure automation using Terraform, and I’ve also managed microservices on Kubernetes. I really enjoy building end-to-end solutions — from setting up CI/CD pipelines with ArgoCD and GitHub Actions to ensuring deployments are smooth and reliable.**

**Right now, I’m working as a Cloud Architect, where I design scalable, secure, and highly available 3-tier applications on AWS. One of my recent projects involved building a custom data lake using S3, Glue, Athena, and OpenSearch — and I also implemented disaster recovery for legacy applications to improve business continuity.**

**Overall, I’m passionate about designing efficient cloud architectures and continuously improving automation and reliability across systems.”**

---


##### Cloud-Native Data Lake Implementation (AWS S3 + Athena + Glue)
- **Problem:**  
    Our organization was dealing with large volumes of structured data from multiple sources. Traditional ETL pipelines and reporting systems were slow, batch-oriented, and required heavy infrastructure. This caused long reporting times and prevented stakeholders from getting real-time insights for decision-making.   
- **Solution:**  
    I designed and implemented a **cloud-native data lake** using **AWS S3** for centralized storage, **AWS Glue** for schema discovery and ETL, and **Amazon Athena** for serverless querying. This serverless architecture eliminated the need for managing infrastructure, provided on-demand querying, and allowed near real-time analytics at scale.
- **Impact:**  
    This solution reduced reporting time by **70%**, enabled **ad-hoc and near real-time analytics**, and gave business stakeholders faster, data-driven decision-making capabilities—all while lowering operational costs compared to traditional systems.


### How to design scalable, secure, and highly available 3-tier applications in AWS?
#### **The STAR Method Framework**

Use the **STAR** method (Situation, Task, Action, Result) to structure your response:

#### **Sample Interview Response Structure:**

**"I've designed several scalable 3-tier architectures in AWS. Let me walk you through my approach using a recent project as an example."**

---

#### **1. Start with Context (Situation & Task)**

**"In my previous role at [Company], we needed to migrate a monolithic application to AWS with requirements for:**

- **99.95% availability**
- **Handling 10x traffic spikes during peak seasons**
- **SOC 2 compliance for security**
- **Cost optimization without compromising performance**

**My task was to design and implement a 3-tier architecture that met these requirements."**

---
#### **2. Explain Your Design Approach (Action)**
##### **First, Lay the Foundation:**

**"I started with a multi-AZ VPC architecture with:**

- **Public subnets** for web tier (Load Balancers, NAT Gateways)
- **Private subnets** for application tier
- **Isolated subnets** for database tier
- **3 Availability Zones** for high availability"
    
##### **Then, Detail Each Tier:**
###### **Web Tier:**
**"For the web tier, I used:**
- **Application Load Balancer** with cross-zone load balancing
- **Amazon CloudFront** with WAF for DDoS protection and caching
- **Route 53** for DNS failover between regions
- **Auto Scaling groups** to handle traffic fluctuations"
#### **Application Tier:**

**"The application tier was designed using:**
- **ECS Fargate** for serverless container management
- **Horizontal scaling** based on CPU utilization and request count
- **Session state externalized** to ElastiCache Redis
- **Immutable infrastructure** patterns with blue-green deployments"
    
#### **Database Tier:**
**"For data persistence:**
- **Aurora MySQL** with read replicas for read-heavy workloads
- **DynamoDB** for high-velocity data with auto-scaling
- **Backup strategies** including automated snapshots and Point-in-Time Recovery
- **Database proxies** for connection management"

---

#### **3. Highlight Key Design Principles (What Interviewers Want to Hear)**

##### **Scalability:**

**"I ensured scalability through:**
- **Horizontal scaling** rather than vertical
- **Stateless application design**
- **Database read replicas** and caching layers
- **Queue-based decoupling** using SQS for asynchronous processing"
    
##### **Security:**

**"Security was implemented via defense in depth:**
- **Network ACLs** and **Security Groups** for network segmentation
- **IAM roles** instead of access keys for applications
- **Secrets Manager** for credential management
- **Encryption at rest** and in transit
- **Regular security assessments** and compliance monitoring"
##### **High Availability:**

**"For high availability, I designed:**

- **Multi-AZ deployments** across all tiers
- **Health checks** and automatic failover
- **Circuit breaker patterns** in application code
- **Disaster recovery** with automated failover to secondary region"    

---

#### **4. Demonstrate Practical Implementation (Show Your Hands-on Experience)**

##### **Mention Specific AWS Services:**

**"In implementation, I used:**
- **Infrastructure as Code** with CloudFormation/Terraform
- **CI/CD pipeline** using CodePipeline and CodeDeploy
- **Monitoring** with CloudWatch alarms and dashboards
- **Cost optimization** through Reserved Instances and Spot Fleets"
##### **Give Concrete Examples:**

**"For example, one challenge was database connection management. I solved this by:**

- Implementing **RDS Proxy** to handle connection pooling
- Using **ElastiCache** to reduce database load
- Configuring **appropriate timeouts** and retry logic in the application"

---
#### **5. Quantify Your Results**

**"The results of this architecture were:**
- **99.99% uptime** achieved (exceeded the 99.95% target)
- **60% reduction in infrastructure costs** compared to on-premises
- **Ability to handle 15x traffic spikes** without performance degradation
- **Faster deployment cycles** - from weekly to multiple deployments per day
- **Improved security posture** with automated compliance reporting"
    

---

#### **6. Common Interview Questions & How to Answer**

##### **"How do you handle database failover?"**

**"I use Aurora Multi-AZ with automated failover. The key is:**

- Monitoring replication lag
- Having application-level retry logic
- Using RDS Proxy for seamless connection failover
- Regular DR drills to test the process"
##### **"How do you ensure security between tiers?"**

**"Through layered security:**

- Security Groups with minimum required ports
- Network ACLs for subnet-level protection
- IAM roles for service-to-service authentication
- VPC endpoints to avoid public internet exposure"
    
##### **"How do you monitor this architecture?"**

**"Comprehensive monitoring with:**
- CloudWatch for metrics and logs
- X-Ray for distributed tracing
- Custom dashboards for business metrics
- Automated alerts with appropriate thresholds"

---

#### **7. Pro Tips for Interview Success**

##### **Do:**

- ✅ **Use specific AWS service names** (not just "load balancer" but "Application Load Balancer")    
- ✅ **Mention real numbers** (latency improved from X to Y, costs reduced by Z%)
- ✅ **Discuss trade-offs** you considered (cost vs. performance, simplicity vs. features)
- ✅ **Show learning from mistakes** ("We initially had issue X, but solved it by Y")
- ✅ **Ask clarifying questions** about their specific environment
    

##### **Don't:**

- ❌ **Oversimplify** ("I just used Auto Scaling")
- ❌ **Forget about costs** (always mention cost optimization)
- ❌ **Ignore operational aspects** (monitoring, logging, troubleshooting)
- ❌ **Use buzzwords without understanding** (explain why you chose microservices/lambda/etc.)    

---

## **Sample Concise Answer (30-60 seconds):**

**"I design 3-tier architectures focusing on scalability, security, and high availability. For the web tier, I use CloudFront and ALB with WAF protection. The application tier typically runs on ECS/EKS with auto-scaling, while the database tier uses Aurora with read replicas. Everything is deployed across multiple AZs with proper security groups, IAM roles, and encryption. I've implemented this pattern for [mention specific project] resulting in 99.99% availability and handling 10x traffic spikes."**



- What you achieved and what challenges you face.

###### 30-Second version(Elevator pitch)

I designed an active-passive multi-region EKS setup with a primary cluster in Region A
(us-east-1) and DR cluster in Region B (us-west-2).
We used AWS Global Accelerator with Route53 for traffic failover, ArgoCD for GitOps-based state synchronization, and Aurora Global Database plus S3 cross-region replication for shared data. In case of failture, we promote the secondary Aurora, switch traffic with Global Accelerator, and unpause ArgoCD in the DR region to active workloads.

###### Detail version (2-3 minutes, deep dive)
I have designed an active-passive multi-region EKS setup for disaster recovery. We deployed identical eks cluster in two AWS region. The primary cluster runs production traffic, while the DR cluster remains passive but synchronized using ArgoCD GitOps, so manifest are always up-to-date.
For traffic management we used AWS Global Accelerator with static anycast IPs, combined with Route53 health checks and failover routing. 
Container images are stored in ECR with cross-region replication, ensuring both clusters can pull the same images.
On the data side, we use Aurora Global Database for relational workloads, with Region A as the writer and Region B as the read replica, which can be promoted during DR. We also configure S3 cross-region replication for object storage and DynamoDB Global Tables for low-latency distributed access if required. Secrets and encryption keys are replicated with AWS Secrets Manager and multi-region KMS keys.
In case of failure, our DR runbook includes promoting Aurora to primary, shifting traffic via Glabal Accelerator, and enabling workloads in Region B by unpausing ArgoCD sync. We regularly test this failover process to validate our [[RTO]]/[[RPO]]. This approach ensures high availability, business continuity, and resilience against regional outages.

###### Follow-up Questions:

1. **Why did you choose active-passive instead of active-active?**
Ans:- Active-passive keeps architecture simpler and avoids data cosisency challenges. It also reduce cost since only one cluster actively serves traffic, while the other is on standby. For our workload, quick failver with Aurora Global DB and Global Accelerator met the RTO/RPO without the comlexity of active-active confict resolution.

**Q: How do you keep the both clusters in sync?**
ans: - We use ArgoCD with GitOps. Application manifests live in Git, and ArgoCD deploy them to both clusters. The DR cluster stays in sync but with critical workloads paused. This ensure DR can be activated quickly with no drift between environments.

**Q: How is data consistency handled across regions?**
ans:- For relational data we have Aurora Global Database, which provides near real-time replication and quick promotion of secondaries. For Objects , S3 cross-region replication ensures availability, and for NoSQL we use DynamoDB Tables. This gives us low RPO while avoiding manual sync.

Q: What's the failover process during a disaster?
Ans: If Region-A goes down, we promote Aurora in Region-B to Primary, switch Global Accelerator endpoind weights or Route53 records to DR, and unpause ArgoCD to activate workloads in the DR cluster. The process is scripted and tested in DR drills.

**Q: How do you handle secrets and encryption across regions?**
ans: We use AWS Secrets Manager with cross-region replication enabled, and all secrets are encrypted with KMS multi-region keys. This Ensures secrets are always available and consistent in both clusters.

Q: How do you test failover?
ans: We schedule regular DR drills. During tests, we simulate primary region failure, run the automated promotion of Aurora, Shift Global Accelerator/Route 53 traffic, and activate workloads in DR. We measure actual RTO/RPO against defined objectives to validate readiness.

**Q: What are the challenges with multi-region EKS?**
ANS: The main challenges are cost, data replication latency, and avoiding drift between clusters. We mitigate this with GitOps for state sync, Aurora Global DB for low-latency replication, and periodic DR drills to validate the design.

**Q : How do you manage container images in DR region?**
Ans: We use Amazon ECR with cross-region replication enabled. This ensures that any images pushed in the primary is automatically available in the DR region without manual sync.

**Q: What happens when the primary region recovers?**
Ans: We carefully fail back; First, we sync data from DR Aurora back to the primary, restore replication, then gradually switch traffic back via Global Accerator Or Route53. Workloads are resynced via ArgoCD to ensure consistency.

**Q: How to do you ensure security and IAM across clusters?**
We enable IRSA in both clusters with OIDC providers per region, using least-privilege IAM roles. Cross-account/region roles are used for replication tasks. Secrets and encryption keys are managed with multi-region KMS keys for consistent access policies.



Recent task performed on organization:
Company was using on prem database in some of part of application.
I propose to use Aurora database instead of on prem DB which was integral part of the application. and Build the report engine by desidning custom data lake in s3 where we use aws glue, athena and penhato tool as etl.
For database migration we use aws dms service, for networking site to site vpn was configure along with aws direct connect service, applicatin migration was taking care of other team.

---


As part of a large-scale cloud modernization initiative, I contributed to two key areas — **database modernization** and **data lake implementation**.

**1. Database Modernization:**  
I proposed and led the migration of the company’s on-premises MySQL database to **Amazon Aurora MySQL**, which was a core component of the application stack. The goal was to improve scalability, availability, and performance while minimizing infrastructure management. The migration was executed using **AWS Database Migration Service (DMS)** to ensure minimal downtime and maintain data integrity. For secure hybrid connectivity, I configured a **Site-to-Site VPN** and **AWS Direct Connect** between the on-premises data center and AWS.

**2. Custom Data Lake Implementation:**  
To address business reporting and data archival requirements, I designed and implemented a **custom data lake on Amazon S3**. The data lake was integrated with **AWS Glue** for data cataloging and transformation, **Amazon Athena** for serverless querying, and **Pentaho** as the ETL and reporting layer. This setup streamlined analytics and enabled efficient, cost-effective data access across teams.