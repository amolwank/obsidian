- Blue Green Deployment is a release strategy used to deploy applications with zero downtime.
- You keep two environments:
	- Blue = Current running version (live and receiving traffic).
	- Green = New version (deployed, but not receiving traffic yet)
When the green environment is tested and verified, traffic is switched from blue -> green instantly.