## **Static Anycast IP Addresses - Complete Overview**

**Static Anycast** is a networking technique where the **same IP address** is announced from **multiple geographic locations**, and traffic is automatically routed to the **nearest/optimal endpoint** based on [[BGP]] routing protocols.

## **How Anycast Works:**

### **Basic Principle:**
```
Same IP: 203.0.113.1
           ↓
┌─────────┬─────────┬─────────┐
│ NYC     │ London  │ Tokyo   │
│ Server  │ Server  │ Server  │
└─────────┴─────────┴─────────┘

User in Paris → Routes to London (nearest)
User in SF → Routes to NYC (nearest)
User in HK → Routes to Tokyo (nearest)
```

## **Key Characteristics:**

### **"Static" vs Regular Anycast:**

```
Regular Anycast:
  - IP can move between locations
  - Dynamic routing changes
  - Common in CDNs, DNS

Static Anycast:
  - IP is permanently assigned to multiple locations
  - Stable endpoint identification
  - Used for critical services
```


## **AWS Implementation:**

### **1. Global Accelerator**

```
# Terraform example
resource "aws_globalaccelerator_accelerator" "main" {
  name            = "my-global-accelerator"
  ip_address_type = "IPV4"
  enabled         = true

  attributes {
    flow_logs_enabled   = true
    flow_logs_s3_bucket = "my-flow-logs-bucket"
    flow_logs_s3_prefix = "flow-logs/"
  }
}

resource "aws_globalaccelerator_listener" "main" {
  accelerator_arn = aws_globalaccelerator_accelerator.main.id
  client_affinity = "NONE"
  protocol        = "TCP"

  port_range {
    from_port = 80
    to_port   = 80
  }

  port_range {
    from_port = 443
    to_port   = 443
  }
}

resource "aws_globalaccelerator_endpoint_group" "main" {
  listener_arn = aws_globalaccelerator_listener.main.id

  endpoint_configuration {
    endpoint_id = aws_lb.main.arn
    weight      = 100
  }

  # Health checks from multiple regions
  health_check_port = 80
  health_check_protocol = "TCP"
  
  endpoint_group_region = "us-west-2"
}

# This provides static anycast IPs:
# - Two static anycast IPs assigned
# - Same IPs across all regions
# - Traffic routed to nearest healthy endpoint
```

---

## **Cost Considerations:**

### **AWS Global Accelerator Pricing:**
```
Fixed Costs:
  - $0.025 per hour per accelerator
  - $0.025 per hour for each custom routing listener

Data Transfer:
  - $0.01 to $0.04 per GB (region dependent)
  - No charge for traffic between Accelerator and endpoints
```

## **Interview Questions & Answers:**

### **Q: What's the difference between anycast and load balancing?**

**A:** "Load balancing distributes traffic across multiple servers **within a datacenter**, while anycast distributes traffic across multiple **geographic locations** using BGP routing. Anycast operates at Layer 3, while load balancers typically operate at Layer 4 or 7."

### **Q: When would you use static anycast IPs?**

**A:** "For **global services requiring stable endpoints** - like DNS servers, VPN concentrators, global APIs, or DDoS protection services. The static IPs provide predictable endpoints while anycast routing ensures optimal performance and availability."

### **Q: How does anycast handle stateful connections?**

**A:** "Anycast can break stateful connections if a client gets routed to different locations. Solutions include:

- **Client affinity** based on source IP
    
- **Session synchronization** between locations
    
- **Sticky sessions** at application layer
    
- Using anycast only for stateless services like DNS"
    

### **Q: Can you use anycast with HTTPS?**

**A:** "Yes, through **TCP anycast** (like AWS Global Accelerator). The TLS handshake happens with the nearest endpoint. For advanced features like SNI-based routing, you'd combine anycast with Layer 7 load balancing."

### **Q: What are the limitations of anycast?**

**A:** "**State management challenges**, **potential for routing instability** (BGP flapping), **complex troubleshooting** due to multiple locations, and **cost** for maintaining global infrastructure."

---

## **Key Advantages Summary:**

- **🌍 Global Reach**: Single IP works worldwide
    
- **⚡ Low Latency**: Automatic optimal routing
    
- **🛡️ DDoS Resilience**: Traffic absorption at edges
    
- **🔧 High Availability**: Automatic failover
    
- **📈 Scalability**: Distribute load geographically
    

Static anycast IPs are essential for building **globally resilient, high-performance services** that appear as a single endpoint to users while being distributed across multiple locations worldwide.

## **Short Answer:**

**Static Anycast IPs** are single IP addresses advertised from multiple global locations. Traffic automatically routes to the nearest endpoint via BGP, providing:

- **Low latency** (users reach closest location)
    
- **High availability** (automatic failover)
    
- **DDoS protection** (attack traffic absorbed at edges)
    
- **Simplified DNS** (single IP for global service)
    

**Examples:** AWS Global Accelerator, Cloudflare (1.1.1.1), Google DNS (8.8.8.8)

**Use cases:** Global APIs, DNS services, VPN endpoints, and any service needing reliable global access.