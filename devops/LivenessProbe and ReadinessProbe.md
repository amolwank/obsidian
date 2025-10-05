## 🔎 Liveness Probe

- **Checks if the container is alive (running properly)**.
- If it fails → Kubernetes **kills the pod** and restarts it.
- Use case: If an app is stuck (e.g., deadlock, infinite loop).

👉 _Analogy_: Checking if a person is still **breathing**. If not → revive.

---
## 🔎 Readiness Probe
- **Checks if the container is ready to serve traffic**.
- If it fails → Pod is kept **out of Service endpoints**, so it won’t get traffic.
- Use case: App still starting up, or temporarily overloaded.

👉 _Analogy_: A person is alive but **not ready to work** yet.

---

## 🛠️ Probe Types in Kubernetes

Both probes can check using:

- **HTTP** → e.g., `/healthz` endpoint    
- **TCP** → check if a port is open
- **Command** → run a command inside container

---

## 📝 Easy to Remember

- **Liveness = Alive?** (restart if dead)    
- **Readiness = Ready to serve?** (remove from load balancer if not)
---

In **Kubernetes manifests**, the **livenessProbe** and **readinessProbe** are defined inside the **`containers` section** of a Pod/Deployment spec.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-app:latest
        ports:
        - containerPort: 8080

        # 🔎 Probes are defined here
        livenessProbe:
          httpGet:
            path: /healthz
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5

        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 3
```

## 📝 Key Notes to Remember

- Both probes go **inside each container definition** (not at Pod level).
- **`initialDelaySeconds`** → wait before first check (gives app time to start).
- **`periodSeconds`** → how often to check.
- **`httpGet`, `tcpSocket`, or `exec`** → the way to perform the check.

👉 So the probes are **part of the container spec in the manifest**.