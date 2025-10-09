
---

### 🔹 **What is the Need for API Gateway?**

An **API Gateway** acts as a **single entry point** for clients to access backend services or microservices. It simplifies, secures, and manages API calls.

### 🔹 **Why We Need It:**
1. **Centralized API Management**
    - Provides a single endpoint to manage multiple APIs.
    - Helps versioning, monitoring, and throttling.
2. **Security**
    - Supports authentication (Cognito, JWT, API keys).
    - Can enforce throttling, rate limits, and IP restrictions.
3. **Protocol & Transformation**
    - Translates protocols (HTTP ↔ WebSocket, REST ↔ Lambda).
    - Can transform request/response payloads.
4. **Scalability & Reliability**
    - Handles large numbers of concurrent requests.
    - Integrates with backend services like Lambda, EC2, or containers.
5. **Monitoring & Logging**
    - Tracks metrics, latency, errors, and request logs.
    - Helps debugging and optimizing API performance.

---
### 🔹 **Protocols API Gateway Supports**

- **HTTP/HTTPS** → Standard web protocols.
- **WebSocket** → Real-time two-way communication.
- **REST** → Application-level protocol over HTTP.
- **gRPC (via HTTP API)** → For high-performance microservices communication (AWS supports through HTTP APIs).

### 🔹 **Common Use Cases:**
- Serverless applications with **AWS Lambda**.
- Exposing microservices in a **secure and controlled manner**.
- Mobile or web apps needing a **single API entry point**.
- Rate-limiting or caching API requests to reduce backend load.
---

✅ **Interview One-liner:**  
“API Gateway provides a secure, scalable, and managed entry point for clients to access backend services, enabling centralized API management, authentication, throttling, and monitoring.”

---

API Gateway is a service that acts as a single entry point for multiple services or APIs.

In practical way,
Think of it like the reception desk of a building:
- Visitors (Users, apps) come to the reception.
- The receptionist (API Gateway) decides where to send them (which service or backend system)
- It also checks ID (authentication), keeps logs, and applies rules.

![[Pasted image 20250912182504.png]]

https://blog.algomaster.io/p/what-is-an-api-gateway

Key Features of API Gateway
- Request Routing -> Forwards incoming requests to the correct backend service (like microservices, databases, Labda functions).
- Security -> Handles authentication, authorization, API Keys, rate limiting etc.
- Protocol Translation-> Converts between different formats(e.g. HTTP to websocket, REST to gRPC)
- Monitoring  and Logging -> Tracks usage, collect metrics, and logs errors.
- Traffic Management-> Can throttle requests, load balance, and cache responses for faster results.