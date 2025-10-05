Cluster Info and Context
```
kubectl version
kubectl cluster-info                 -> Display cluster control plan info.
kubectl get nodes                    -> List all nodes in the cluster.
kubectl config get-contexts          -> List kubeconfig contexts. 
kubectl config use-context <context> -> Switch to a specific context.
```

Working with Pods:
```
kubectl get pods
kubectl get pods -n <namespace>
kubectl describe pod <pod-name> -> Show detailed pod info.
kubectl logs <pod-name>         -> View pod logs. 
kubectl exec -it <pod-name> -- /bin/sh -> Open shell inside the pod.
kubectl delete pod <pod-name>
```
Deployments:
```
kubectl get deployments
kubectl describe deployment <deployment-name>
kubectl scale deployment <name> --repplicas=3 -> Scale replicas.
kubectl rollout status deployment/<name> -> Check rollout status
kubectl rollout undo deployment/<name> -> Rollback deployment.
```
Services:
```
kubectl get svc -> List services
kubectl describe svc <service-name> -> Details about a service.
kubectl expose deployment <name> --type=NodePort --port=80 -> Expose deployment as service
```

Namespaces:
```
kubectl get ns
kubectl create namespace <ns-name> ->Create a namespace
kubectl delete ns <ns-name>
```
Config and Secrets:
```
kubectl get configmap -> List configmaps
kubectl describe configmap <name> -> Show configmap details
kubectl get secret -> List secrets
kubectl describe secret <name> -> Show secret details.
```
Apply and Manage Manifests:
```
kubectl apply -f file.yaml
kubectl delete -f file.yaml
kubectl get all -> Get all resources in current namespace
```

Debugging:
```
kubectl describe pod <pod-name> -> Detailed events and info.
kubectl logs <pod-name> -> Logs of pod.
kubectl get events --sort-by=.metadata.creationTimestamp ->Check recents events
kubectl top pod -> show CPU/memory usage (needs Metrics Server)
```
