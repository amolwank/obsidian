### **What are Parallel Jobs?**
- In GitHub Actions, a **job** is a set of steps that runs on a runner.
- **Parallel jobs** mean multiple jobs in a workflow can **run at the same time**, instead of waiting for one job to finish before starting the next.
- This speeds up the CI/CD pipeline and reduces overall runtime.
    
---
### **Key Points**

- Jobs can run **concurrently** if they do **not have dependencies** (`needs` keyword is used to set dependencies).
- Each job can have its **own runner**, environment, and steps.
- Parallelization is ideal for **independent tasks**:
    - Running **unit tests** for multiple services simultaneously
    - Building **Docker images** for multiple microservices at the same time
    - Linting and testing in parallel
---

### **Example Workflow**
```
name: Parallel Jobs Example

on:
  push:
    branches: [main]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Linter
        run: npm run lint

  unit_tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Unit Tests
        run: npm test

  build_docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker Image
        run: docker build -t my-app:latest .
```