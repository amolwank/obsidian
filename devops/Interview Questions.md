Empetus Round 1:
1. How you design scalable and highly available microservice.- [[Scalable and highly available Design]]
2. What the significance of VPC?
3. Which AWS AI services you have used? - [[AWS AI Services]]
4. What all are the key points you will consider while migrating application from on-reprem to cloud.?
5. How you will design the hybrid application in AWS cloud?
6. 
AWS:
How do you choose monolithic vs michroservice arhitecture?
How you make your applications secure?
- AWS Shield
- WAF
- Least privileges access.
What cost optimization major you will take for cost sensitive client?
For Compute:
- Select right EC2 instance type (memory intensive, GPU intensive)
- Reserve Instance Plans
- We can use the spot instances
For Storage:
- Right S3 storage classess.
- Select right Storage for EBS use gp3 instead of gp3
- We should not use highly iops base volumes if not needed.
For Data transfer cost:
- VPC Endpoint for private connectivity
What AWS Services you will use for on-prem servers to connect to AWS Instractructure?
- Site to Site VPN Connectivity withing VPN
- Customer gateway and 
- Make use of Direct connect which a physical lines/cabels which connect to aws data center
-

Kubernetes Questions:
What is Statefulset ?
- pod will have identity
- can be associated with persistent volume

How you create multi-state docker build?
- allows us to use multiple From Statement
- Allows us to copy only useful artifacts
- Helps in complex build process
- Build a minimal build image
- Helps us create optimize image

What error you  face or how you debug kubernetes application?
- crashloopbackerror - pod goes to pending state, 
- it might be due to not able to fetch the image
- get event pods to get the events of the pods
- We can describe the pod if there any misconfigutaion 
- Not able to fetch the secrets due to permission issues
- Node is not having the enough resources.

Terraform Questions:

1. Why you will use custom modules even though we have official modules are available for use.
2. How you use dynamic block and if yes what was the usecase?
3. 
[[20 AWS Solution Architect Scenario-Based Interview Q&A]]

[[20 Important Kubernetes Interview Questions]]
[[CICD Interview Questions (Senior Level)]]

