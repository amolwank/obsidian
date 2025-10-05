These control how Pods communicate and expose themselves.
- [[Service]] -> Stable networking endpoints for pods.
- Ingress -> HTTP/HTTPS routing to services. 
- IngressClass -> Defines the type/config of an Ingress controller.
- Endpoint / EndpointSlice ->Stored actual Pod IPs behind a Service
- NetworkPolicy -> Controls allowed network traffic.