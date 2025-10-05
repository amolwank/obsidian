###### Kubernetes Architecture (High-Level)
1. Control Plane (Master) 
	- Manages the whole cluster
	- Components
		- kube-apiserver -> Communication hub (brain)
		- etcd -> Cluster state database
		- kube-scheduler -> Decides where pods run.
		- kube-controller-manager -> Ensures desired state.
		- cloud-controller-manager -> Cloud integrations.
2. Worker Nodes
	- Run the actual apps (Pods).
	- Components:
		- kubelet -> Talks to control plane, manages pods
		- kube-proxy -> Networking, load balancing.
		- container runtime -> Runs containers (Docker, containerd. CRI-O)
		
Kubernetes follows a master-worker (control plane & node) architecture.
```
             +------------------------+
             |   Control Plane (API)  |
             |------------------------|
             |  kube-apiserver        |
             |  etcd                  |
             |  kube-scheduler        |
             |  kube-controller-mgr   |
             +-----------+------------+
                         |
   --------------------------------------------------
                         |
         +---------------+----------------+
         |                                |
+-------------------+             +-------------------+
| Worker Node       |             | Worker Node       |
|-------------------|             |-------------------|
| kubelet           |             | kubelet           |
| kube-proxy        |             | kube-proxy        |
| Container Runtime |             | Container Runtime |
| (Docker/containerd)|            | (Docker/containerd)|
| Pods (App1, App2) |             | Pods (App3, App4) |
+-------------------+             +-------------------+
```
###### Components:
**Control Plane (Master Components):**
Responsible for managing the cluster
- kube-apiserver
	- Fontend of Kubernetes (REST API)
	- All communication (kubectl, nodes, controllers) goes through API server.
- etcd
	- Key-value store that keeps the cluster's state & configuration.
	- Example: Which pods run on which node.
- kube-scheduler
	- Assigns pods to nodes based on resources, affinity, taints/tolerations.
- kube-controller-manager
	- Runs controllers that manages cluster state:
		- Node controller (Monitors nodes)
		- Replication controller (ensures correct pod count)
		- Endpoint controller etc

**Worker Node Components**
Where applications (Pods/containers) actually run
- kubelet
	- Agent on each node
	- Talks to API server and makes sure containers (Pods) are running as expected.
- kube-proxy
	- Handles networking/routing.
	- Ensures services can talk to pods (ClusterIP, NodePort, LoadBalancer).
- Container Runtime
	- Runs the containers (Docker, containerd, CRI-O)
	- Kubernetes itself does not run containers; it uses runtime underneath.
###### Pods
- The smallest deployable unit in kubernetes.
- A Pod can have 1 or more containers that share:
	- Network (IP)
	- Storage (Volumes)

###### Additional Concepts
- Namespace -> Logical separation within a cluster (like folders)
- Deployment -> Manages replicas of pods.
- Service -> Provides stable networking to Pods.
- Ingress -> Manages external HTTP/HTTPS access.
###### Flow of Operations:
1. User runs a command (e.g. kubectl apply -f deployment.yaml)
2. kubectl ->sends request to API server.
3. API server stores desired state in etcd.
4. Scheduler decides which node will run the new pod.
5. kubelet on that node instructs the container runtime to run containers.
6. kube-proxy ensures networking between pods and services.

