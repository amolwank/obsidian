We can optimize the cost without affecting performance.

1. Right-Sizing Resource
	- Analyse EC2, RDS, and other services for underutilization using [[AWS Cost Explorer]] or [[Compute Optimizer]].
	- Stop or downsize instances with low CPU/ memory usage.
	- Use [[Auto Scaling]] to match demand instead of over-provisioning.
	- For dev/test workloads, consider [[Spot Instances]] or similar instance families.
	
2. Use [[Reserved Instances (RIs)]] and [[Saving Plans]]
	- For workloads running 24/7 (like production databases or web apps), use
		- Compute Saving Plans (flexible, covers EC2, Farget, Lambda).
		- Reserved Instances (If workload is predictable and steady).
	- This can cut costs by 30-70% compared to On-Demand.
3. Storage Optimization
	- Use [[S3 Lifecycle Policies]] to move data from Standard -> Infrequent Access ->Glacier ->Deep Archive
	- Delete Old versions if versioning is enabled.
	- Compress and deduplicate files before uploading.
	- For EBS:
		- Delete unused volumes
		- Use gp3 instead of g2 (cheaper, better performance)
		- Take snapshot and delete unused volumes
4. Monitor and Control Idle Resources
	- Shutdown dev/test environments outside of business hours (use lambda or Instance Scheduler)
	- Identify unused Elastic IPs, Load Balancers and NAT Gateways.
	- Clean up old snapshots, AMIs, and unattached EBS Volumes.
5. Leverage Serverless & Managed Services
	- Use Lambda,  Farget, or DynamoDB for workloads with unpredictable traffic.
	- Managed services often cost less than managing EC2-based solutions.
6. Optimize Data Transfer Costs
	- Use VPC Endpoints to avoid NAT Gateway charges.
	- Keep services in the same region/AZ to reduce data transfer.
	- Use CloudFront as a CDN to reduce S3/EC2 data transfer charges.
7. Use AWS Cost Management Tools
	1. [[AWS Budgets]] -> Set alerts when costs exceed thresholds.
	2. [[Cost Anomaly Detection]] -> Identify unexpected cost spikes.
	3. [[Cost Explorer]] -> Track spending patterns.
8. Governance and Policies
	1. Enforce tagging policies to track costs by project/team.
	2. Use Service Control Policies (SCPs) to restrict expensive services.
	3. Educate teams to design with cost efficiency in mind (Part of [[AWS Well-Architected Framework]]).

Review:
Cost Optimization:
?
1. Right-Sizing Resource
2. Use Reserved Instances and Saving Plan
3. Storage Optimization
4. Monitor and Control Idle resource
5. Leverage Serverless and Managed services
6. Optimize Data Transfer Cost
7. Use AWS Cost Management Tools
8. Governance and Policies
#flashcards
<!--SR:!2025-09-22,3,268-->
