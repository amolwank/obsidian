**What is AWS Cost Anomaly Detection?**
- Its a AI-powered service from AWS that uses machine learning to automatically find unexpected changes in your cloud spending.
- Instead of you manually checking bills, it learns your usage patterns and alerts you when something unusual happens(e.g. sudden spike in S3 consts or EC2)

**Key Features**
- ML-based detection -> Learns from your past 14+ days of cost/usage data
- Granularity -> Works at:
	- Linked accounts (for organization)
	- Services (like EC2, S3, RDS)
	- Linked account + service combination
- Notification -> Integrate with Amazon SNS to send alerts to email, slack ro ticketing systems.
- Automatic leaning ->No needs to set thresholds; it adopts to usage over time.

###### How IT Works
- Create an Anomaly Detection Monitor
	- Define scope: entire AWS account, a linked account, or a single service.
- Create an Anomaly Detection Subscription
	- Tell AWS how you want to be notified. (SNS, email, etc)
- Machine Learning kicks in;
	- AWS analyse your historical spending patterns
	- Detect deviations (too high or too low)
- Get Alters
	- Example: If your S3 bill suddenly jumps from $50/day to $200/day, it sends you an alert

Cost:
Free to use -> AWS does not charges for Cost Anomaly Detection itself
You only pay for SNS notifications (very minimal).

In Short: AWS Cost Anomaly Detection = AI watchdog for your AWS bills.
It won't directly reduce cost but will help you catch abnormal costs early, so you can act before the monthly bill explodes.