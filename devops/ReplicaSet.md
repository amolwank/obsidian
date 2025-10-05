A ReplicaSet in Kubernetes is a controller that ensures a specific number of identical Pods are always running.

A [[Deployment]] automatically creates and manages a ReplicaSet for us.

When would you define a ReplicaSet directly?
- Rarely, mostly for:
	- Learning/demo purposes
	- Very static workloads where you dont need rolling pdates or rollback