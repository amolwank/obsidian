A ConfigMap is a Kuabernetes object that is used to store configuration data in key-value pairs.
Instead of hardcoding config values (like database url app setting) inside containers, you keep them in a ConfigMap.
Your Pods/Containers can then use these values at runtime.