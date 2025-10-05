Create a new Helm Chart
```
helm create mychart
```
This generates a structure like

```
mychart/
	Chart.yaml      # Metadata (name, version etc)
	values.yaml     # Default configuration values.
	charts/         # Dependencies (other charts)
	templates/      # Kubernetes manifest templates
	.helmignore     # Files ignored by Helm
	
```
