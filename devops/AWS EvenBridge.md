**EventBridge** is a serverless **event bus** that lets you connect different applications and AWS services using events, enabling you to build reactive, decoupled architectures.

---
![[Pasted image 20251003092101.png]]

### The Core Concept: It's an Event Router
Think of it as the **nervous system** or a **postal service** for your applications. Instead of services calling each other directly (tight coupling), they send events to EventBridge, which then reliably routes them to the correct targets.

### Key Use Cases (Why You Use It)

1. **Decouple Microservices:** Service A doesn't need to know about Service B. It just emits an "OrderPlaced" event. EventBridge routes it to Service B, which handles shipping.
    
2. **Integrate SaaS Applications:** You can receive events directly from third-party SaaS apps like Shopify, Datadog, or Auth0 and trigger AWS workflows in response (e.g., a new Shopify order triggers a Lambda function).
    
3. **Schedule Cron Jobs:** It can replace traditional cron servers by triggering Lambda functions or other services on a schedule (e.g., "every day at 2 AM").
    
4. **Build Event-Driven Architectures (EDA):** It's the core service for creating systems that react to state changes, making them more scalable and resilient.
    

### How It Works in 3 Steps

1. **Producers emit events** (e.g., an EC2 instance state change, a custom application event, a payment confirmation from Stripe).
    
2. **EventBridge receives the event** on an **event bus**.
    
3. **Rules you define** evaluate the event and **route it to a target** (e.g., a Lambda function, an SQS queue, an SNS topic, or another AWS service).
    

---

### Interview Cheat Sheet

|Aspect|Description|
|---|---|
|**What it is**|A serverless event bus service.|
|**Core Function**|To route events from sources to targets based on rules.|
|**Key Benefit**|Decouples services for scalable, resilient architectures.|
|**Main Use Cases**|1. Microservices communication  <br>2. SaaS app integration  <br>3. Scheduled tasks (cron)  <br>4. Building event-driven systems.|

**Perfect for a quick, confident answer:**
_"EventBridge is AWS's serverless event bus. You use it to build decoupled, event-driven applications by having services publish events to it, and it routes those events to the correct consumers based on rules you define. It's great for connecting your own apps, AWS services, and even third-party SaaS tools."_
