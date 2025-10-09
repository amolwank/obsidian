AWS Config is a service that helps you track, audit, and evaluate the configurations of your AWS resources.

**30s Answer:**  
AWS Config is a service that continuously monitors and records AWS resource configurations, checks them against compliance rules, and can even auto-remediate issues. For example, it can detect if an S3 bucket is public or if an EBS volume isn’t encrypted, and trigger a Lambda to fix it. I’ve used it to enforce tagging policies and ensure compliance during audits by providing a full history of resource changes.

**60s Answer:**  
AWS Config is a service that gives visibility into how AWS resources are configured and ensures they remain compliant with security and governance standards. It continuously records resource configurations and evaluates them against predefined or custom rules.

For example, you can use it to check if **S3 buckets block public access**, **EBS volumes are encrypted**, or if **IAM users have MFA enabled**. If a resource is non-compliant, Config can trigger automatic remediation using **AWS Systems Manager documents or Lambda functions**.

In one of my projects, I used AWS Config across multiple accounts to enforce **tagging policies** for cost allocation and to ensure **compliance with security baselines**. It also helped during audits, since we could easily show historical configuration changes of critical resources.

In short, AWS Config provides **continuous compliance, governance, and auditing** while enabling automatic remediation of misconfigurations.


Here's a simple breakdown:
What it does:
- Records the current configuration of your AWS resources.
- Continuously monitors changes in configurations.
- Stores configuration history for auditing and compliance.

Use cases:
- Security & Compliance -> Ensure S3 buckets are not public, IAM policies are not overly permissive, etc.
- Auditing -> Maintain a history of resource configurations for audits
- Troubleshooting -> Identify changes that caused an issue. (e.g. why an instance stopped working).
- Automation -> Trigger remediation actions using AWS Lambda when non-compliance is detected.
Example:
If you set a rule that "All S3 buckets must have encryption enabled," AWS Config will continuously check buckets. If someone create an unencrypted bucket, it will flag it as non-compliance, and you can even trigger an automatic fix (e.g. apply encryption).