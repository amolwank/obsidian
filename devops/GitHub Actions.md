**GitHub Actions** is **GitHub's built-in automation and CI/CD platform** that lets you automate workflows directly inside your GitHub repository.
[[Have you used the GitHub Action in your project?]]
[[Parallel Job]]

Here are the **most important aspects to highlight in an interview**:

---

### 🔹 Core Concepts

- **Workflow basics:** Defined in `.github/workflows/*.yml`. Triggered by events (push, pull_request, schedule, manual).
- **Jobs & steps:** Jobs run in parallel (by default), each job has steps that run sequentially.
- **Runners:** Workflows run on GitHub-hosted runners (like `ubuntu-latest`) or self-hosted runners.
- **Actions:** Reusable units of code (from GitHub Marketplace or custom).
    

---

### 🔹 CI/CD Use Cases

- **CI:** Run tests, linting, build Docker images, run Terraform `validate/plan`.
    
- **CD:** Deploy to AWS (ECS, EKS, Lambda), GCP, Azure, or on-prem.
    
- **Infrastructure:** Trigger Terraform workflows or Ansible playbooks.
    

---

### 🔹 Key Interview Points

1. **Triggers (Events):**
    - On push, pull request, release, or scheduled cron jobs.
    - Example: run tests on every PR, deploy only on `main` branch.
        
2. **Environment Management:**
    
    - Use environments (dev, staging, prod) with approvals.
    - Protect production deployments with manual approvals.
        
3. **Secrets & Security:**
    
    - Store credentials in **GitHub Secrets**.
    - Mask secrets in logs.
    - Use OIDC + AWS IAM roles for short-lived credentials (instead of static keys).
        
4. **Caching & Performance:**
    
    - Cache dependencies (npm, pip, Docker layers, Terraform plugins) to speed up builds.
        
5. **Parallelism & Matrix Builds:**
    
    - Run jobs in parallel (e.g., test multiple versions of Python/Node).
        
6. **Reusable Workflows:**
    
    - Use `workflow_call` to centralize CI/CD logic across multiple repos.
        
7. **Artifacts & Logs:**
    
    - Store build/test artifacts for debugging or deployment.
        

---

### 🔹 How to Answer in Interview (1-min summary)

_"GitHub Actions is a CI/CD platform built into GitHub. I’ve used it to automate Terraform deployments and application pipelines. Workflows are defined in YAML and triggered by events like pushes or pull requests. Each workflow has jobs and steps that can run on GitHub-hosted or self-hosted runners. I follow best practices like using GitHub Secrets for credentials, caching dependencies for speed, running jobs in parallel, and separating dev/staging/prod environments with approval gates. This has helped me achieve reliable, automated deployments while keeping pipelines secure and efficient."_


What it does?
- Automates tasks like building, testing, and deploying your code.
- Runs when certain events happen (e.g. code push, pull request, issue created)
- Use YAML configuration files (.github/workflow/*.yaml)* stored in your repo.

Key Features:
- CI/CD Integration: Automatically test code after each commit or PR.
- Event-driven: Workflows trigger on events like push, pull_request or on schedules (cron)
- Runner ->Jobs runs on GitHub-hosted servers (Linux,Windows,macOS) on your own self-hosted servers.
- Reusable Workflows: Share and reuse workflows across multiple repos.
- [[Marketplace]]: Thousands of prebuilt actions (e.g. deploy to AWS, send slack notifications).

Basic Workflow Structure:
```
name: Workflow Name           # Optional, friendly name

on:                           # Trigger events
  push:
    branches: [main]          # Trigger on push to main
  pull_request:
    branches: [main]          # Trigger on PR to main

jobs:                         # Defines the jobs
  job_id:                     # Unique ID for the job
    name: Job Friendly Name   # Optional, display name
    runs-on: ubuntu-latest    # Runner environment

    steps:                    # Series of steps to execute
      - uses: actions/checkout@v3   # Checkout code
      - name: Run Linter
        run: npm run lint
      - name: Run Tests
        run: npm test
```


Example Workflow (YAML)

```
name: CI Pipeline

on: [push, pull_request]

jobs:
	build:
		runs-on: ubuntu-latest
		steps:
			- name: Checkout code
			  uses: actions/checkout@v3
			  
			- name: set up node.js
			  uses: actions/setup-node@v4
			  with:
				  node-version: '18'
			- name: Install Dependencies
			  run: npm install
			
			- name: Run tests
			  run: npm test  
	  
```
4️⃣ Example with Parallel Jobs and Dependency

```
name: CI/CD Pipeline

on:
  push:
    branches: [main]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm run lint

  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm test

  build_and_deploy:
    runs-on: ubuntu-latest
    needs: [lint, test]          # Waits for lint & test jobs to finish
    steps:
      - uses: actions/checkout@v3
      - run: docker build -t my-app:latest .
      - run: docker push my-app:latest
```

**Explanation:**
- `lint` and `test` run **in parallel**.
- `build_and_deploy` runs **after both** finish, because of `needs`.