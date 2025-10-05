A Chart **is a collection of files** that describes a related set of Kubernetes resources.
It's the packaging format used by Helm to define, install, and upgrade complex Kubernetes applications.

Key Characteristics of Helm charts:
- Package Format ->
- Directory Structure-> A chart is organized as a specific directory structure containing;
	- Chart.yaml (metadata about the chart)
	- values.yaml (default configuration values)
	- templates/ - directory (Kubernetes manifest templates)
	- Other optional files like README.md, NOTES.txt, etc.
- Templating ->Charts use Go templates, allowing parameterization of Kubernetes manifiests.
- Versioning-> Charts can be versioned and dependencies between charts can be specified.
[[Step by Step Guide]]: