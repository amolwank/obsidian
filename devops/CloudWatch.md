Amazon CloudWatch is AWS's monitoring and observability service.
it collects metrics, logs, and events from AWS Services, applications and custom sources.

**Interview Ready Answser:**
Amazon CloudWatch is AWS's obervability service. It collects metrics, logs, and events from AWS services and custom applications. I can create alarms, visualize dashboards, and even trigger automated actions like Auto scaling or Lambda execution. For example, in our multi-region EKS setup, we used CloudWatch container Insights to monitor cluster health and application performace, and integrated alarms with SNS to notify the team during incidents.

**Key Features:**
-  Metrics: CPU, memory, network, latency, etc. (From AWS resource + custom metrics)
- Logs: Collects and stores application/system logs (e.g. EC2, Lambda, EKS pods).
- Alarms: Trigger alarms or automated actions (like scaling, notifications) when thresholds are crossed.
- Dashboards: Visualize metrics & logs in real time.
- Events (EventBridge): React to system or application state changes automatically.
- CloudWatch Agent: Install on EC2/On-prem to push OS-level metrics and logs.
- Integration: Works with Auto scaling, SNS, Lambda, System Manager, etc,

**Example Use Cases:**
- Monitor EC2 CPU usage, trigger Auto Scaling when CPU > 80 %.
- Collect application logs from EKS Pods, analyze them centrally.
