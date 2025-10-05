Key Areas of AWS Cloud Security:
1. Identity & Access Management (IAM)
	1. Use IAM users, groups, roles, policies
	2. Follow least privilege (give only required permissions).
	3. Enable MFA (Multi-factor authentication).
	4. Use IAM Roles instead of long-lived access keys
	5. AWS Services
		1. IAM
		2. AWS Organizations +SCPs
		3. AWS SSO
2. Data Protection
	- Encryption at rest
		- S3, EBS, RDS, Redshift -> Support KMS-managed keys.
	- Encryption in transit:
		- Use HTTPS/TLS, enforce SSL on buckets.
	- AWS Secrets Manager / Parameter Store -> store API keys, passwords security
3. Network Security
	- VPC -> Isolated virtual network.
	- Security Groups- Virtual firewalls at instance level.
	- NACLs -> Subnet-level stateless firewalls.
	- Private Subnets -> Keep sensitive resources (databases) away from the public internet.
	- AWS Shield -> DDoS protection.
	- WAF -> Protect against SQL injection, XSS, bots
	- VPC Flow Logs -> Monitor traffic
4. Monitoring & Threat Detection
	- CloudTrail -> Logs every API call (who did what)
	- CloudWatch -> Monitoring, metrics, alerts.
	- GuardDuty -> Threat detection (malware, crypto, mining, suspicious API calls).
	- Security Hub ->Central security dashboard (aggregates GuardDuty, Inspector, Macie findings)
	- AWS Inspector -> Scans EC2/ECR for vulnerabilities.
	- AWS Macie -> Identifies sensitive data (like PII) in S3.
5. Application Security
	- CodePipeline + CodeBuild + CodeDeploy -> Integrate security checks in CI/CD.
	- ECR image scanning ->Check container images for vulnerabilities.
	- API Gateway + WAF -> Secure APIs.		
6. Governance & Compliance
	- AWS Config -> Track resource configurations & compliance
	- Service Control Policies (SCPs) ->Restrict accounts from doing unsafe actions.
	- Conformance Packs -> Predefined compliance templates.
7. Disaster Recovery & Backup
	- Use S3 Versioning + MFA Delete to prevent accidental/malicious deletions.
	- AWS Backup -> Centralized backup service.
	- Cross-region replication (S3, RDS) for disaster recovery.

###### Best Practices Summary:
- Enable MFA for all accounts
- Use IAM roles (no root/long-term keys)
- Encrypt everything (S3, EBS, RDS)
- Place databases in private subnets.
- Enable CloudTrail + GuardDuty + Config for visibility.
- Apply SCPs for guardrails across accounts.
- Regularly review security findings in Security Hub.