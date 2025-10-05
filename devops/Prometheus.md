Prometheus is an **open-source monitoring and alerting tool** designed for metrics-based monitoring.
-> meaning it collects numerical time-series data like CPU usage, request counts, memory usage and stores it for querying and alerting.

Originally built at SoundCloud. It is now standalone open source project and maintained independently of any company.

Prometheus joined the [[Cloud Native Computing Foundation]] in 2016 as the second hosted project after Kubernetes.

Key Features
- Time-series database ->
- Powerful query language (PromQL)
- Pull-based model
- No dependency on external storage
- Alerting
- Kubernetes native

How It Works
1. Targets (applications/services) exposes metrics on an HTTP endpoint (e.g. /metrics)
2. Prometheus server scrapes these endpoints periodically.
3. Data is stored in Prometheus's time-series database.
4. You can query metrics using PromQL or visualize them in [[Grafana]].
5. Alerts are sent if certain conditions are met (via Alertmanager).

Example Use Case
- Monitor Kubernetes cluster health.
	- Node CPU usage
	- Pod memory usage
	- API server request latency
- Detect anomalies and trigger alerts
- Create Grafana dashboards for real-time visualisation.

Run Prometheus in Docker
```
docker run -p 9090:9090 prom/prometheus
```
