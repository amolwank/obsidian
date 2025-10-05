# High-level goals

- **Scalable:** handle increased load automatically (horizontal scale preferred).
    
- **Highly available:** tolerate failures of instances, AZs, even regions if required.
    
- **Resilient & observable:** fast recovery, good visibility, and graceful degradation.
    
- **Secure and cost-aware.**
    

---

# Core design decisions (short)

- Make services **stateless** where possible. Keep state in external stores.
    
- Use **horizontal autoscaling** (more instances) rather than vertical.
    
- Use **multiple Availability Zones (AZs)** — replicate across AZs.
    
- Decouple components using **asynchronous messaging** for resiliency.
    
- Use **managed services** where feasible (DB, queuing, caching) to reduce ops.
    

---

# Recommended architecture components (AWS-flavored)

- **Ingress / API layer**
    
    - API Gateway or Application Load Balancer (ALB) + TLS termination.
        
    - WAF in front for protection.
        
- **Compute**
    
    - Container platform: Amazon EKS (Kubernetes) or ECS/Fargate for containers.
        
    - Or serverless: AWS Lambda for event-driven small services.
        
    - Run at least 2+ replicas across AZs.
        
- **Autoscaling**
    
    - HPA (K8s) / ECS Service AutoScaling / Lambda concurrency-based scaling.
        
    - Use metrics (CPU, memory, request latency, custom business metrics).
        
- **Service discovery & routing**
    
    - Kubernetes Service / CoreDNS or AWS Cloud Map.
        
    - Client-side load balancing (if needed) or rely on platform LB.
        
- **Data layer**
    
    - For relational: Amazon Aurora (multi-AZ, read replicas, Aurora Global DB for cross-region).
        
    - For key-value: Amazon DynamoDB (managed, multi-AZ, DynamoDB Accelerator for caching).
        
    - For caching: Amazon ElastiCache (Redis) or DAX for DynamoDB.
        
- **Messaging / queueing**
    
    - SQS / SNS for decoupling, retries, backpressure.
        
    - For high-throughput/event streams: Amazon MSK (Kafka) or Kinesis.
        
- **File / object storage**
    
    - Amazon S3 for attachments, artifacts, immutable objects.
        
- **Observability**
    
    - Metrics: CloudWatch / Prometheus + Grafana.
        
    - Tracing: AWS X-Ray or OpenTelemetry (distributed tracing).
        
    - Logging: structured logs to CloudWatch Logs / ELK / OpenSearch.
        
    - Alerts: CloudWatch alarms / PagerDuty.
        
- **Resilience patterns**
    
    - Circuit breaker, retries with exponential backoff, bulkhead isolation, timeouts.
        
    - Rate limiting & throttling at API Gateway/edge.
        
- **Deployment / CI-CD**
    
    - Infrastructure as Code: Terraform / CloudFormation / CDK.
        
    - CI/CD: GitHub Actions, CodePipeline, or Jenkins with blue/green or canary deployments (ArgoCD for k8s).
        
- **Security**
    
    - Least-privilege IAM roles, KMS for secrets, AWS Secrets Manager or HashiCorp Vault.
        
    - Network isolation: VPC subnets, security groups, private services in private subnets.
        
    - Mutual TLS or mTLS for service-to-service where needed.
        
- **Backups & DR**
    
    - Automated backups for DB, cross-region replication for critical services.
        
    - RTO/RPO defined and tested via DR runbooks.
        

---

# Detailed design patterns & best practices

- **Stateless service**: keep session state in Redis/DynamoDB or issue signed tokens (JWT).    
- **Idempotency**: for operations that may be retried, use idempotency keys.
- **Graceful shutdown**: respect SIGTERM, finish/stop accepting new requests, drain connections.
- **Horizontal partitioning (sharding)**: for very large datasets, shard by tenant or key.
- **Read replicas & CQRS**: separate read-heavy queries to read-replicas or build a read-model.
- **Throttling & backpressure**: protect downstream with rate limiting and queueing.
    
- **Feature flags**: for controlled rollouts and quick rollback.
    
- **Autoscaling safeguards**: use target tracking but limit min/max instances and cooldowns.
    
- **Chaos testing**: simulate failures (terminate nodes, inject latency) to verify resilience.
    

---

# Operational checklist (keep this handy)

- Health checks (Liveness & Readiness) for every service.    
- Circuit breaker thresholds and retry policies defined per dependency.
- SLO/SLA/SLIs defined (e.g., 99.9% availability, p95 latency < X ms).
- Centralized logging + searchable traces for request flows.
- Automated canary/blue-green deployments with quick rollback.
- Regular load/performance testing to validate autoscaling and capacity.
- Cost monitoring and budget alerts.

---

# Metrics to monitor (important ones)

- Traffic: requests/sec, concurrent requests.    
- Latency: p50/p95/p99 request latency.
- Errors: 4xx/5xx rates per service.
- CPU/Memory of pods/instances.
- Queue length (SQS), consumer lag (Kafka).
- DB metrics: connections, CPU, read/write latency.
- Throttles, retries, and circuit-breaker opens.
    
---
# Example small blueprint (2-minute mental image)

1. Client → CloudFront (optional) → API Gateway / ALB → service A (EKS pods x3 across AZs).
2. Service A calls Service B via internal service DNS; communicates asynchronously via SQS for long jobs.
3. Reads served from Aurora read-replicas + Redis cache. Writes to Aurora primary.
4. Logs → CloudWatch / OpenSearch; traces → X-Ray/OpenTelemetry; metrics → Prometheus + Alerting.
5. CI/CD pipeline deploys to staging, runs canary in prod, and promotes on success.

---

# When to go multi-region

- If required by compliance, very low RTO, or global latency requirements: use active-active or active-passive across regions with data replication (Aurora Global DB / multi-region DynamoDB or custom replication). This increases complexity — do it only when necessary.
    

---

# Quick do/don’t list

- Do: design for failure, automate everything, test regularly.
    
- Don’t: rely on a single AZ or single instance; avoid putting state in local disk; don’t ignore observability.