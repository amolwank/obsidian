- A namespace in kubernetes is like a folder or virtual cluster inside your Kubernetes cluster.
- It helps organize resources and separate environments within the same cluster.
Think of it as different compartments inside one big box (the cluster).

Why Use Namespaces?
1. Organization -> Group related resources (e.g. all dev pods vs prod pods)
2. Access Control -> Apply RBAC (Role Based Access Control) per namespace.
3. Resource Limits -> Set quotas (CPU, memory) per namespace to avoid one team consuming everything.

#flashcards 
