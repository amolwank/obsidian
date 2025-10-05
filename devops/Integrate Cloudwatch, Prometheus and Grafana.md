
---

# 🔹 **60-sec Answer (Crisp)**

- **CloudWatch**: Use **Container Insights** and **FluentBit/CloudWatch Agent** DaemonSet on EKS to ship logs & metrics.
    
- **Prometheus**: Deploy **Prometheus** (often via Helm + Prometheus Operator) to scrape metrics from pods, services, and kubelet.
    
- **Grafana**: Deploy **Grafana** (self-hosted in EKS or use Amazon Managed Grafana). Connect it to both **Prometheus** and **CloudWatch** as data sources.  
    👉 Together: CloudWatch gives AWS-native visibility & alarms; Prometheus gives fine-grained Kubernetes metrics; Grafana unifies dashboards.
    

---

# 🔹 **2–3 min Answer (Detailed)**

In EKS, we usually need **end-to-end observability** across cluster, workloads, and AWS infrastructure. I’d design it as follows:

### 1. **CloudWatch Integration**

- Enable **CloudWatch Container Insights** → deploy the **CloudWatch agent + FluentBit DaemonSet** on each node.
- Collects:
    - Cluster-level metrics (CPU, memory, disk, network per pod/node).
    - Logs (application logs, control plane logs) → shipped to CloudWatch Logs.
- Use **CloudWatch Alarms** for critical metrics and **CloudWatch Logs Insights** for queries.

### 2. **Prometheus Integration**

- Deploy **Prometheus Operator (kube-prometheus-stack Helm chart)** inside EKS.
- Scrapes metrics from:
    - `kubelet`, `kube-state-metrics`, and application pods exposing `/metrics`.    
    - AWS components (via CloudWatch exporter, if needed).    
- Prometheus handles **real-time alerting** with Alertmanager.

### 3. **Grafana Integration**
- Option 1: Deploy Grafana as a pod inside EKS.
- Option 2: Use **Amazon Managed Grafana** (no maintenance, integrates with IAM & CloudWatch easily).
- Configure **data sources**:
    - Prometheus → for pod-level & app-level metrics.   
    - CloudWatch → for AWS infra & managed services (RDS, ALB, S3, etc.).    
- Create **dashboards** (cluster health, node utilization, request latency, error rates, custom SLOs).
### 4. **Best Practices**

- Use **IRSA** (IAM Roles for Service Accounts) for Prometheus/Grafana/FluentBit to access CloudWatch securely.
- For **multi-account or multi-cluster** monitoring, centralize CloudWatch logs/metrics in one account + federated Grafana.
- Set up **alerts** in both CloudWatch (infra-level) and Prometheus (app-level) → route via SNS, Slack, or PagerDuty.
    

---

# 🔑 **Memory Trick**

Think of it as **3 layers**:
- **CloudWatch → AWS-native visibility** (infra, managed services).
- **Prometheus → Kubernetes-native metrics** (pods, workloads).
- **Grafana → Unified dashboards** (one pane of glass).
    

---

⚡ Example 1-line in an interview:

> “I integrate CloudWatch for infra metrics/logs, Prometheus for pod-level scraping, and Grafana as a single dashboard across both, often using Amazon Managed Grafana for ease of IAM integration.”