A Service is like a reception desk -  no matter how often staff (Pods) change, you always call the same number, and the receptionist connects you to whoever is available.

In kubernetes, a Service is a way to give a stable network address to your Pods so other apps can reach them.

Since Pods can be created, destroyed, or moved between nodes, their IPs keep changing- a Service acts like a permanent phone number that always points to the right Pods.

**Key Points**
- Load balances traffic between multiple pods
- Keeps the same IP and DNS name even if Pods change
- Can make Pods accessible inside the cluster (internal) or outside (external)

**Types of Services**
- ClusterIP -> default, reachable only inside the cluster
- NodePort -> exposes the service on a fixed port of every node
- LoadBalancer -> uses a cloud provider's load balancer to make it public
- ExternalName -> maps to an external DNS name

Example:
```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80       # Service port
      targetPort: 8080  # Pod port
  type: ClusterIP

```






Tags: #Kubernetes