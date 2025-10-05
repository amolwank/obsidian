Kubernetes Main Components
1. Control Plane
	1. kube-apiserver -> The Brain that processes commands
	2. etcd -> Key-value store for cluster state
	3. kube-scheduler -> Assigns pods to nodes
	4. Kube-controller-manager -> Handles replications, scaling, etc
2. Worker Nodes
	1. kubelet -> Talks to control plane, runs containers
	2. kube-proxy -> Manages networking rules
	3. Container Runtime ->Docker, Containerd, etc