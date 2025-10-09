### The One-Sentence Answer

**AWS GuardDuty** is an intelligent **threat detection service** that uses machine learning and threat intelligence to continuously monitor your AWS accounts and workloads for malicious or unauthorized activity.

---

### The Core Concept: Your AWS Security Guard

Think of GuardDuty as a **24/7 security guard** for your AWS environment. It doesn't prevent attacks itself, but it's constantly watching your logs and network traffic, looking for known attack patterns and suspicious behavior, and then **alerting you** when it finds something.

### What It Actually Monitors

GuardDuty analyzes billions of events from multiple AWS data sources without you needing to manually configure them:

1. **AWS CloudTrail Event Logs:** For suspicious API calls (e.g., an API call from a known malicious IP address, or a user doing something they never have before).
2. **VPC Flow Logs:** For unusual network traffic (e.g., communication with a known command-and-control server, or a port scan from within your VPC).
3. **DNS Logs:** For malicious domain activity (e.g., an EC2 instance querying a domain known for cryptocurrency mining).
    

### Key Use Cases (Why You Use It)

1. **Intrusion Detection:** It identifies compromised EC2 instances, containers, or IAM credentials that are being used maliciously.
    
2. **Threat Intelligence:** It uses continuously updated threat intelligence feeds (like lists of known malicious IPs and domains) to spot known bad actors.
    
3. **Anomaly Detection:** Its ML models learn your normal baseline and flag significant deviations (e.g., "This IAM user is suddenly launching instances in a region they've never used before").
    
4. **Compliance & Visibility:** It provides a centralized view of potential security issues across your accounts, which is crucial for security audits and compliance frameworks.
    

---

### How It Works in 3 Steps

1. **You Enable It:** It's a simple one-click enablement in the AWS console (region-specific). There are no agents to install.
    
2. **It Analyzes:** It automatically starts analyzing CloudTrail, VPC Flow, and DNS logs from your account.
    
3. **You Get Findings:** It generates **security findings** (like "UnauthorizedAccess:EC2/MaliciousIPCaller") with a severity level (Low, Medium, High) that you can view in the console or send to **Amazon EventBridge** for automated remediation (e.g., trigger a Lambda function to isolate a compromised instance).
    

---

### Interview Cheat Sheet

|Aspect|Description|
|---|---|
|**What it is**|An intelligent, managed threat detection service.|
|**Core Function**|Continuously monitors for malicious and unauthorized behavior.|
|**Key Benefit**|Provides actionable security findings with context and no operational overhead.|
|**Data Sources**|CloudTrail Logs, VPC Flow Logs, DNS Logs.|
|**Main Use Cases**|1. Detecting compromised resources  <br>2. Identifying reconnaissance activity  <br>3. Monitoring for anomalous behavior  <br>4. Meeting compliance needs.|

**Perfect for a quick, confident answer:** "GuardDuty is AWS's managed threat detection service. It uses ML and threat intelligence to continuously analyze your CloudTrail, VPC Flow, and DNS logs for malicious activity, like cryptocurrency mining, credential compromise, or reconnaissance. You simply enable it, and it starts delivering prioritized security findings."