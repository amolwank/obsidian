What is ArgoCD?
- Argo CD is a declarative , GitOps based CD tool for kubernetes.
- It continuously syncs the desired state (from Git) with the actual state (in Kubernetes cluster).
In Short:
You define your app/deployment manifests in Git and Argo CD automatically ensures your cluster matches what's in Git.

Argo CD is a Kubernetes application itself.
When you install it (via Helm, kubectl or Operator), it creates pods that run inside a namespace (commonly argocd)