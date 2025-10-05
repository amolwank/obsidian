Integration patterns are standard ways to connect different systems, services, or applications so they can exchange data reliably and efficiently

Example: You Order service needs to talk to Payment Service -> How do they integrate? REST? Messaging? That's where integration patterns come-in.

Common Integration Patterns
1. Synchronous (Request/Response)
	- One service calls another and waits for a reply
	- E.g. Rest API call from Order Service -> Payment Service
	- Simple and real-time
	- Can fail if the other service is down.
2. Asynchronous Messaging
	- Service communicated via a message broker (Kafka, RabbitMQ, AWS SQS).
	- Sender doesn't wait for response, just sends a message.
	- Loose coupling, reliable
	- Harder to debug.
3. Event-Driven (Pub/Sub)
4. File Transfer
5. Shared Database
6. Database per Service + Data Replication
7. API Gateway Pattern
8. Aggregator Pattern
9. Circuit Breaker Pattern
	- Prevents cascading failures. If one service is down, calls "break" and return fallback.
	- Improves resilience
10. Saga Pattern (For transaction)
	- Used in distributed systems where multiple services are involved in a transaction.
	- Example: Placing an order involves Payments, Inventory, Shipping.
	- Saga ensures consistency by chaining compensating actions if something fails.
Real life Example (E-commerce Order)
- User places order -> API Gateway -> Order Service
- Order Service publishes event ->Payment service & Inventory Service
- Payment success -> Notification service sends confirmation
- If Payment fails -> Saga triggers rollback (Inventory release, order cancelled)