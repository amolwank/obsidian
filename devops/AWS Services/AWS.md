Introduction:
AWS(Amazon Web Services) is a cloud computing platform provided by Amazon.
It offers on-demands services like computing power, storage, networking, databases analytics, machine learning, and more - all delivered over the network.

[[AWS Security Services]]:
###### Key Points:
- Launched: 2006 by Amazon.
- Pay-as-you-go model: You pay only for what you use.
- Global Infrastructure: AWS has data centers worldwide (called Regions and Availability Zones)
- Scalability: can scale up or down resources quickly based on demand.
- Security:Provide identity management, encryption, compliance certificates.

[[Well Architected Framework]]

[[API Gateway and LoadBalancer]]
###### Major AWS Services:
- Compute
	- [[EC2]] (Elastic Compute Cloud) -> Virtual Server
	- [[Lambda]] -> Serverless computing (run code without managing servers)
	- [[ECS]]/[[EKS]] -> Container services
- Storage:
	- [[S3]] (Simple Storage Service) ->Object storage
	- [[EBS]] (Elastic Block Store) -> Disk storage for EC2
	- [[Glacier]] ->Archival storage
- Databases:
	- [[RDS]] (Relational Database Service).
	- [[DynamoDB]] (NoSQL database).
	- [[Redshift]] (Data warehouse).
- Networking and Security:
	- [[VPC]] (Virtual Private Cloud)
	- [[Route 53]] (DNS)
	- [[IAM]] (Identity and Access Management).
- Monitoring and Tools:
	- [[CloudWatch]] (Monitoring).
	- [[CloudTrail]] (Audit logs).
	- [[CloudFormation]] / Terraform (Infrastructure as code) 

Main Services:
[[AWS Route53]]
[[AWS GuardDuty]]
[[AWS Control Tower]]
[[AWS Global Accelerator]]
###### [[Cloud Security in AWS]]:
AWS follows the shared Responsibility Model:
- AWS secures the infrastructure (data centers, hardware, networking)
- You (the customer) secure what you run on top of AWS (Apps, data, IAM, configs)
[[Cost Optimization]]
[[AWS Step Functions]]
[[AWS Organizations]] -> is a service that lets you centrally manage multiple AWS accounts. 
[[API Gateway ]]-> API Gateway is a service that acts as a single entry point for multiple backend services or APIs
[[AWS Bedrock]]
[[AWS X-Ray]]
[[AWS SQS]]
[[AWS Config]]
[[AWS CloudFront]]
🛠️ [[Ways to Manage Multiple AWS Accounts]]

[[Designing E-commerce app]]

How to [[trace logs or any activity happening in AWS accounts]]?
[[AWS WAF]]
[[AWS EvenBridge]]
[[AWS System Manager]]
[[AWS IAM Identity Center]]
## 🔹 **Core AWS Architecture & Design**

1. How would you design a **multi-region, highly available architecture** in AWS? - [[Multi-region, highly available architecture in AWS]]
2. What are the trade-offs between **monolith vs. microservices** in AWS?
3. How would you design a **hybrid cloud setup** (on-prem + AWS)? - [[Hybrid Cloud Setup]]
4. How do you handle **DR (Disaster Recovery)** – what strategies (Pilot Light, Warm Standby, Active-Active) would you use?
5. How would you migrate a **large-scale on-prem application** to AWS?

---
## 🔹 **Networking & Security**
6. Explain how you’d design a **secure VPC** for a multi-tier app. - [[Secure VPC]]
7. Difference between **NACLs, Security Groups, and WAF** – when to use what?
8. How do you set up **cross-account access** securely in AWS Organizations?
9. [[Explain Transit Gateway vs. VPC Peering vs. PrivateLink]].
10. How would you design a **zero-trust network** in AWS?

---
## 🔹 **Compute & Scaling**
11. How would you choose between **ECS, EKS, and Lambda** for an application? -[[ECS, EKS, and Lambda]]
12. How do you design for **auto-scaling across multiple AZs and regions**?
13. How do you ensure **cost optimization** while scaling workloads?
---
## 🔹 **Storage & Databases**

14. How do you decide between **RDS, DynamoDB, and Aurora**?
15. How would you design a **multi-region data replication** strategy (Aurora Global DB, DynamoDB Global Tables, S3 CRR)? - [[Multi-region data replication strategy]]
16. How do you secure **S3 buckets** and enforce compliance (encryption, IAM, SCP, bucket policies)?

---
## 🔹 **Monitoring, Logging, and Reliability**

17. How do you set up **observability** (CloudWatch, X-Ray, OpenTelemetry, Prometheus, Grafana)?
18. How do you implement **chaos engineering** or simulate failure in AWS?
19. What’s your strategy for **handling noisy neighbors** in a shared infra setup?
---
## 🔹 **Cost & Governance**
20. What’s **FinOps** in AWS? How do you monitor and optimize cloud spend?
21. How do you enforce compliance rules across all accounts (Config, SCP, Control Tower)?
22. How do you track and manage **shared services (logging, networking, security accounts)**?
---

## 🔹 **Scenario-Based**
23. If a region goes down, how would you ensure **business continuity**?    
24. How would you design a **global application with low latency** for users across US, Europe, and Asia?
25. A developer accidentally exposed an S3 bucket – how do you **detect, respond, and prevent** such incidents?
26. How do you design **CI/CD pipelines** for multi-account, multi-region deployments?
27. You have **100+ AWS accounts** – how would you manage **IAM, security, and cost control** efficiently?
---

✅ **Tip to Prepare:**
- Senior-level interviews are **50% scenario + 50% design trade-offs**.
- Always answer using **Well-Architected Framework pillars**: **Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability**.

[[AWS Senior Level Interview Cheat Sheet]]