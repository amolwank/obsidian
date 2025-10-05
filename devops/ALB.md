What is ALB (Application Load Balancer)?
- ALB is an AWS Layer 7 load balancer (works at HTTP/HTTPS level).
- It automatically distributes traffic across multiple targets (EC2, ECS, EKS, Lambda)
- Supports path-based, host-based, and header-based routing.
- Provides SSL termination, WebSockets, gRPC, and WAF integration.


### 🔹 ALB vs NLB vs CLB (Quick Comparison)

| Feature              | ALB (Layer 7)             | NLB (Layer 4)                       | CLB (Legacy)     |
| -------------------- | ------------------------- | ----------------------------------- | ---------------- |
| Protocols            | HTTP, HTTPS, gRPC         | TCP, UDP, TLS                       | HTTP, HTTPS, TCP |
| Routing              | Path / Host / Header      | Port/Protocol only                  | Basic            |
| Use Case             | Web apps, APIs            | High perf, low latency, gaming, IoT | Legacy apps      |
| Security Integration | WAF, Cognito, SSL offload | Security groups, TLS passthrough    | Basic            |


Interview one-liner:
ALB
?
ALB is a Layer 7 load balancer that provides intelligent routing for web apps, APIs, and microservers, unlike NLB which is Layer 4 and used for high-perfomance TCP/UDP traffic.
<!--SR:!2025-09-21,1,230-->

#flashcards 