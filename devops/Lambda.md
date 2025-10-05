AWS Lambda is a serverless compute service that lets you run code without **provisioning or managing servers.**
###### Key Concepts:
- Event-driven -> Runs code in response to events (API Gateway request, S3 upload, DynamoDB update, CloudWatch, schedule etc) 
- Fully managed -> No need to manage servers, scaling, or OS patching.
- Pay-per-use -> Charged based on numbers of requests + execution duration (in milliseconds)
- Stateless -> Each execution is independent (Can use external storage like s3, DynamoDB or RSD for state.)  
Common Use Cases:
- Running APIs with API Gateway + Lamdba
- Processing S3 events
- Data Pipenline
- Automating infrastructure tasks (e.g. backups, cron jobs with CloudWatch).
Architecture Points:
- Trigger Sources:
- Execution Environment:
- Scaling
- Cold Start  vs Warm Start
	- Cold Start: Extra latency when you start container
	- Warm start: Faster execution when container is reused.
