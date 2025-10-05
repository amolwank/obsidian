"The package manager for kubernetes"

Helm is a tool for managing Kubernetes packages called charts ([[Helm Charts]]).

Helm can do the following:
- Create new charts from scratch
- Packages charts into chart archive(tgz) files
- Interact with chart repositories where charts are stored
- Install and uninstall charts into an existing Kubernetes cluster
- Manage the release cycle of charts that have been installed with Helm

Helm command in shorts:
- helm repo -> Manage repositories
- helm search -> find charts
- helm install/upgrade/uninstall -> manage deployment
- helm template/dry-run -> debug
```
helm version

helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo nginx
# Install a chart
helm install my-nginx bitnami/nginx
helm list
helm stats my-nginx
# Upgrade a release
helm upgrade my-nginx bitnami/nginx --set replicaCount=3

# Rollback to a previous version
helm rollback my-gninx 1

# Uninstall a release
helm uninstall my-nginx

```
Working with values:
```
helm show values bitnami/nginx

# Install with custom values file
helm install my-nginx bitnami/nginx -f values.yaml

# set values inline
helm install my-nginx bitnami/gninx --set replicaCount=2,image.tag=latest
```
Debugging:
```
# Dry run (preview without installing)
helm install my-nginx bitnami/nginx --dry-run --debug
```

```
helm template my-nginx bitnami/nginx

# show chart info

helm show chart bitnami/nginx

```