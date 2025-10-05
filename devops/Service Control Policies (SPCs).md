###### Introduction
- SCPs are a type of policy in AWS Organizations.
- They let you centrally control permissions for all accounts in your organization.
- Think of SCPs as guardrails: they set the maximum permissions an account (or users/roles in that account) can ever have.
![[Pasted image 20250913111808.png]]

###### Key Points:
- SCPs do not grant permissions on their own -> they only restrict what IAM users/roles can do.
- They apply to
	- The root user of the account
	- All IAM users
	- All IAM roles
- By default, every AWS Org has a policy called "FullAWSAccess" (allows everything)
###### Example Use Cases:
- Deny usage of certain services
- Restrict actions to only specific regions
- Prevent disabling important security services like CloudTrail, Config, or GuardDuty.
- Enforce that only approved services/resources are used.