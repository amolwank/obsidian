What is AWS Step Functions?
- AWS Step Functions is a serverless orchestration service.
- It lets you coordinate multiple AWS services (like Lambda, ECS, DynamoDB, S3, Glue, etc) into a workflow.
- A workflow is written as  a state machine (JSON-based definition).
- Each "step" represents a task (like run a Lambda, wait, make a choice, call API).

Think of it as a flowchart builder for AWS services- but it runs automatically in the cloud.

In Interview, you can say:
AWS Step Functions is a serverless workflow orchestration service that coordinate multiple AWS services using state machines. It's useful for building data pipelines, microservice orchestration, and long-running business workflows with built-in error handling and retries.

Simple Example
Imagine you upload an image to S3 and want to process it:
1. Step 1: Trigger Lambda -->Extract metadata
2. Step 2: If Image is > 1 MB --> Compress, else skip
3. Step 3: Save metadata in DynamoDB
4. Step 4: Notify user via SNS.
This whole flow can be automated with a step function without writing big complex code.