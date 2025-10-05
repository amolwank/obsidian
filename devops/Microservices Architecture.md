- It's a way of building software where an application is broken into small, independent services.
- Each service focuses on a specific business function (e.g. user management, payments, orders).
- These services talk to each other using APIs (often REST, gRPC, or messaging queue)

Characteristic of Microservices:
- Independently deployable -> Update one service without touching others.
- Loosely coupled-> Each service works on its own but communicates with others.
- Domain-driven ->
- Technology Freedom -> One service may use Python, another Go, another Java.
- Scalable -> Scale only the service that needs more power.
