A StatefulSet is like a Deployment, but it's designed for applications that require:
- Stable network identity (same DNS name for each pod)
- Stable, persistent storage ( each pod gets its own volume).
- Ordered, predictable deployment & scaling (Pods start/stop in sequence).