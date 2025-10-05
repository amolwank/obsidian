Definition:
A VPC (Virtual Private Cloud) is a logically isolated section of the AWS Cloud where you can launch AWS resources (like EC2 instances, RDS databases, Lambda functions etc.) in a secure and controlled environment.

Key Features:
- Isolation: You get your own private network space.
- IP Addressing: You choose your own IP address range (using CIDR blocks, e.g. 10.0.0.0/16).
- [[Subnets]]: You can divide the VPC into public subnet (accessible from the internet) and private subnets (not directly accessible).
- [[Routing]]: Control how traffic flows inside the VPC using Route Tables.
- Security: Protect resources with [[Security Groups]] (instance-level firewalls) and [[Network ACLs]] (Subnet-level firewalls)
- Connectivity
	- [[Internet Gateway ]](IGT) - for internet access.
	- [[NAT Gateway]] - lets private instances access the internet without being exposed.
	- [[VPC Peering]] - connects multiple VPCs
	- [[VPN]]/[[Direct Connect ]]- connect your on-premise network to AWS.