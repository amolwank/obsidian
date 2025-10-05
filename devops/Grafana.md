Grafana is an open-source data visualisation and analytics platform that lets you turn raw metrics, logs and traces into interactive dashboards and charts.

It's often used with Prometheus (and other data sources) to monitor applications, infrastructure, and business metrics.

Key Features
- Beautiful Dashboards
- Multiple Data Sources
- Custom Queries
- Alerting
- Web-based-UI
- Plugins

How it Works
1. Grafana connects to a data source
2. You write queries to fetch metrics from the data source.
3. Data is visualized using graphs, gauges, pie charts, tables, etc
4. Dashboards can be shared with teams for real-time monitoring.
5. Alerts are triggered if data crosses thresholds.

Common Use Cases
- Kubernetes Monitoring
- Server Monitoring
- Application Performance
- Business Metrics -> Sales numbers, user activity, transactions.

Run Grafana in Docker
```
docker run -d -p 3000:3000 grafana/gafana
```
Default login -> admin/admin
