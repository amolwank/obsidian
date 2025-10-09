AWS Global Accelerator is a networking service that improves the availability, performance and security of your public applications for a global audience.

---
### 🌍 What it is
- A **networking service** that improves the **availability, performance, and global reach** of your applications.
- Provides **[[static anycast IP addresses]]** that act as fixed entry points to your application, even if endpoints (ALBs, NLBs, EC2, EKS, etc.) change.
- Routes traffic over the **AWS global network**, not the public internet, reducing latency and jitter.
---
### ⚙️ How it works
1. User connects to one of the **static anycast IPs** provided by Global Accelerator.
2. Traffic is routed to the **closest AWS edge location** via the [[AWS global backbone]].
3. Accelerator then forwards the traffic to the **healthy and nearest application endpoint** (in one or multiple AWS Regions).
4. It continuously monitors the health of endpoints and automatically reroutes if one fails.

---
### ✅ Use cases
- **Multi-region applications** (e.g., active-active or active-passive failover).
- **Disaster recovery** – automatic failover to backup region.
- **Global applications** – route users to the **nearest region** with low latency.
- **Gaming, SaaS, APIs** – performance-sensitive workloads needing consistent low latency.    
---
### 🔑 Key benefits
- **Improved latency:** routes traffic over AWS backbone.
- **High availability:** automatic failover across endpoints/regions.
- **Static IPs:** no need to update DNS when endpoints change.    
- **Fine-grained routing control:** configure traffic dials (e.g., 70% traffic to us-east-1, 30% to eu-west-1).
- **Integration:** works with ALB, NLB, EC2, EKS, Elastic IPs.
---
👉 In interviews, you can say:  
_"I use AWS Global Accelerator to provide static IPs and route users to the nearest healthy endpoint using the AWS backbone network, which helps reduce latency and ensures high availability across multiple regions."_

Video Ref: https://www.youtube.com/watch?v=uJpIoZTuuv4&t=81s

