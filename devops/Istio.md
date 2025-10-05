- Istio is an open-source service mesh that help manage communication between microservices.
- It runs as a layer on top of Kubernetes and provides traffic management, security, and observability without changing your application code.
**Istio Deployment Modes:**
1. **Sidecar Mode (Default)**
	- Each application Pod has an Envoy sidecar proxy.
	- All inbound and outbound traffic flows through Envoy.
	- Provides fine-grained traffic control, observability, and security.
	- Most common in microservices on Kubernetes.
2. **Gateway Mode**
	- Use Istio Ingress/Egress Gateways (Envoy proxies running as standalone pods).
	- Manages traffice entering (Ingress) or leaving (Engress) the mesh.
	- Example: Controlling API access or outboud traffic to external services.
3. **Ambient Mesh Mode (New in Istio 2022+)**
	- Sidecar-less architecture -> uses ztunnels (zero-trust tunnels) running per node instead of per pod.
	- Simpler, lower overhead, and easier to adopt.
	- Traffic is transparently intercepted and secured.
	- Designed for large-scale clusters where sidecars become heavy.
4. Proxyless Mode (Experimental)
	- Applications integrate Istio features directly using gRPC xDS APIs without Envoy sidercars
	- Used in very specialized performance-critical workloads.

Istio mode (Interview One-liner)
?
"Istio mainly runs in sidecar mode where each pod has an Envoy proxy. It can also run with gateways for ingress/engress traffic, and newer Ambient Mesh mode removes sidecars using node-level proxies for simpler, lower-overhead service mess."

#flashcards 