- HPA (Horizontal Pod Autoscaler) automatically scales the number of Pods in a deployment, replica set, or statefulset based on resource usage (like CPU, memory) or custom metrics.
- Instead of manually setting pod replicas, HPA watches metrics and adjust replicas up or down.
How it Works:
1. HPA checks metrics from metrics Server (must be installed in the cluster)
2. Compares actual usage with the target threshold.
3. Increase or decreases pod replicas accordingly.

Basic Example Manifest:
```
apiVersion: autoscaling/v2
kind: HarizontalPodAutoscaler
metadata:
	name: myapp-ha
spec:
	scaleTargetRef:
		apiVersion: app/v1
		kind: Deployment
		name: myapp-deployment
	minReplicas: 2
	maxReplicas: 6
	metrics:
		- type: Resource
		  resource:
			  name:cpu
			  target:
				  type: Utilization
				  avarageUtilization: 50
```
This means :
- Minimum 2 pods, maximum 6
- HPA  tries to keep average CPU utilization at 50%
Create HPA using kubeclt
```
kubectl autoscale deployment myapp-deployment --cpu-percent=50 --min=2 --max =6
kubectl get hpa
```

Key Points:
- Needs metrics server for CPU/Memory based autoscaling
- Support custom metrics (like request/sec ) via Prometheus + Adapter.
- Works best for stateless workloads.
When to use HPA?
- For applications with variable or unpredictable traffic.
- For Cost optimization (don't run too many pods all the time).
- For ensuring app performance under load.

Quick Note: HPA needs Metrics Server installed in the cluster, otherwise it won't work.