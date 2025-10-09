- AWS X-Ray is a distributed tracing service.
- It helps developers analyze and debug applications, especially micro-services and serverless apps running on AWS.
- It shows how requests flow through your system, making it easier to find bottlenecks, errors, and performance issues.
Think of it a CT scan for your app - You see exactly where requests spend time, and where they fail.

**How AWS X-Ray Works:**
- Instrument your app -> Add X-Ray SDK
- Trace collection -> App sends trace data to X-Ray daemon/agent.
- X-Ray service -> Aggregates traces and build service maps.
- X-Ray console -> You visualize bottlenecks, latency, and errors.

**Example Use Case:**
Imagine an e-commerce app:
- User places an order -> request goes through API Gateway -> Lambda -> DynamoDB ->S3
- X-Ray shows:
	- API Gateway =fast (50 ms)
	- Lambda = slow (400 ms)
	- DynamoDB = normal (20 ms)
	- S3 = failed upload (timeout)

You instantly know the problem is in Lambda's code and S3 communication.