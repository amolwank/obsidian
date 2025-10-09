Good question 👍 — if you have **different endpoints (URLs or APIs)** that need to be served under **one Load Balancer**, AWS **Application Load Balancer (ALB)** handles this using **listener rules** and **target groups**.

Here’s how it works 👇

---
### 💡 **Use Case**

You have multiple endpoints like:

- `/api/orders`
- `/api/users`
- `/app/login`
- `/app/dashboard`

You want them all served through a single domain like `https://myapp.com`.

---
### ⚙️ **Solution: ALB Path-Based Routing**

1. **Create an ALB (Application Load Balancer)**
    - Choose Internet-facing or internal based on your app.
    - Add listeners (usually port **80** for HTTP and **443** for HTTPS).    
2. **Create Target Groups**
    - Create separate **target groups** for each microservice or endpoint.
        - Example:
            - `orders-service-tg`
            - `users-service-tg`
            - `login-service-tg`
            - `dashboard-service-tg`
3. **Define Listener Rules (Path-Based Routing)**
    - Go to **ALB → Listeners → Rules** and add:
        - If path is `/api/orders*` → Forward to `orders-service-tg`
        - If path is `/api/users*` → Forward to `users-service-tg`
        - If path is `/app/login*` → Forward to `login-service-tg`
        - If path is `/app/dashboard*` → Forward to `dashboard-service-tg`
    - Default action → Return 404 or forward to a default target group.
        
4. **(Optional) Host-Based Routing**
    - You can also route based on **domain name** (useful for multiple subdomains):
        - `api.myapp.com` → API target group
        - `app.myapp.com` → Web target group
        - `admin.myapp.com` → Admin target group

---

### 🧠 **Additional Features**

- **Health Checks:** Each target group has its own health check path.
- **Sticky Sessions:** Can be enabled if you need session persistence.
- **SSL Termination:** ALB can manage SSL/TLS certificates via **ACM**.
- **WebSocket & HTTP/2:** Supported natively.
---
### 🧩 **Example Architecture**
```
       Internet
            ↓
     [ Application Load Balancer ]
            ↓
 ┌──────────────────────────────┐
 │  Path Rules                  │
 │  /api/orders  → Orders TG    │
 │  /api/users   → Users TG     │
 │  /app/login   → Login TG     │
 │  /app/dashboard → Dashboard TG │
 └──────────────────────────────┘
            ↓
   [ ECS / EKS / EC2 targets ]
```