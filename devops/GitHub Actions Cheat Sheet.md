# 🧠 **GitHub Actions Cheat Sheet**

## ⚙️ **Basics**

- **Location:** `.github/workflows/` in your repo
    
- **File extension:** `.yml` or `.yaml`
    
- **Triggers:** Define when a workflow runs.
```
name: CI Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:   # Manual trigger
```

---

## 🏗️ **Workflow Structure**

```
name: CI/CD Pipeline

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

## 🚀 **Common Use Cases**

### ✅ **Build & Test**

```
- uses: actions/setup-python@v5
  with:
    python-version: '3.11'
- run: pytest

```


🧱 Docker Build & Push
```
- name: Build Docker image
  run: docker build -t myapp:latest .

- name: Login to DockerHub
  uses: docker/login-action@v3
  with:
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}

- name: Push Image
  run: docker push myapp:latest
```

☁️ **Deploy to AWS (EKS / EC2 / S3)**
```
- name: Configure AWS Credentials
  uses: aws-actions/configure-aws-credentials@v4
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: ap-south-1

- name: Deploy to S3
  run: aws s3 sync ./build s3://my-bucket-name

```

---

## 🧩 **Common Actions**

|Action|Description|
|---|---|
|`actions/checkout@v4`|Clone your repo|
|`actions/setup-node@v4`|Set up Node.js|
|`actions/setup-python@v5`|Set up Python|
|`docker/login-action@v3`|Login to Docker|
|`aws-actions/configure-aws-credentials@v4`|Setup AWS CLI|
|`actions/cache@v4`|Cache dependencies|
|`actions/upload-artifact@v4`|Save build artifacts|
|`actions/download-artifact@v4`|Retrieve artifacts|
🔐 **Secrets and Environment Variables**

```
env:
  REGION: ap-south-1

steps:
  - run: echo "Region is $REGION"
  - run: echo "${{ secrets.MY_SECRET }}"
```
✅ Store secrets under **Repository → Settings → Secrets → Actions**

---

## 🔁 **Matrix Builds (Multiple Environments)**

```
strategy:
  matrix:
    node-version: [14, 16, 18]

steps:
  - uses: actions/setup-node@v4
    with:
      node-version: ${{ matrix.node-version }}

```



---

## 🔄 **Reusable Workflows**

Define reusable file:  
`.github/workflows/deploy.yml`

```
on:
  workflow_call:
    inputs:
      env:
        required: true
        type: string

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to ${{ inputs.env }}"

```

Call it from another workflow:

```
jobs:
  call-deploy:
    uses: ./.github/workflows/deploy.yml
    with:
      env: prod

```


## 🧠 **Best Practices**

- Use **secrets** for credentials.
    
- Use **`actions/cache`** for dependencies.
    
- Use **`workflow_dispatch`** for manual runs.
    
- Split **build**, **test**, and **deploy** into separate jobs.
    
- Add **status badges** in your README.
![CI](https://github.com/username/repo/actions/workflows/main.yml/badge.svg)



---

## 🧰 **Debugging Tips**

- Enable debug logs:
    
    - Add repository secret:  
        `ACTIONS_RUNNER_DEBUG: true`
        
- Add print step:
```
- name: Debug Info
  run: env | sort

```

---
###### ChatGPT said:

Perfect 🔥 — here’s a **ready-to-use DevOps GitHub Actions pipeline** for a **microservice** that builds, tests, containerizes, pushes to Docker Hub, and deploys to **Amazon EKS**.

It’s **production-grade**, modular, and follows **best practices** for CI/CD.

---

# 🚀 **GitHub Actions: Build → Test → Docker → Push → Deploy to EKS**

Create this file:  
📁 `.github/workflows/ci-cd.yml`
```
name: CI/CD Pipeline - Build, Test, Dockerize, and Deploy to EKS

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:   # Manual trigger

env:
  AWS_REGION: ap-south-1
  ECR_REPO: myapp-repo
  IMAGE_TAG: ${{ github.sha }}
  CLUSTER_NAME: my-eks-cluster
  DEPLOYMENT_NAME: myapp-deployment
  CONTAINER_NAME: myapp

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      # 🧾 Step 1: Checkout Code
      - name: Checkout repository
        uses: actions/checkout@v4

      # 🧱 Step 2: Set up Node.js (example for Node app)
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      # 📦 Step 3: Install dependencies and run tests
      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      # 🐳 Step 4: Build Docker Image
      - name: Build Docker image
        run: docker build -t $ECR_REPO:$IMAGE_TAG .

      # 🔐 Step 5: Login to AWS (ECR + EKS access)
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}

      # 🐳 Step 6: Login to ECR
      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      # 📤 Step 7: Push Docker Image to ECR
      - name: Push Image to ECR
        run: |
          docker tag $ECR_REPO:$IMAGE_TAG ${{ steps.login-ecr.outputs.registry }}/$ECR_REPO:$IMAGE_TAG
          docker push ${{ steps.login-ecr.outputs.registry }}/$ECR_REPO:$IMAGE_TAG

      # ☸️ Step 8: Configure kubectl for EKS
      - name: Update kubeconfig
        run: aws eks update-kubeconfig --region $AWS_REGION --name $CLUSTER_NAME

      # 🚀 Step 9: Deploy to EKS
      - name: Deploy to EKS
        run: |
          kubectl set image deployment/$DEPLOYMENT_NAME $CONTAINER_NAME=${{ steps.login-ecr.outputs.registry }}/$ECR_REPO:$IMAGE_TAG
          kubectl rollout status deployment/$DEPLOYMENT_NAME

```

---

## 🔐 **Required GitHub Secrets**

Go to **Repository → Settings → Secrets → Actions**, and add:

|Secret Name|Description|
|---|---|
|`AWS_ACCESS_KEY_ID`|IAM user key with ECR + EKS access|
|`AWS_SECRET_ACCESS_KEY`|IAM user secret|
|_(Optional)_ `DOCKER_USERNAME`, `DOCKER_PASSWORD`|If using DockerHub instead of ECR|


---

## 📘 **How It Works**

1. Triggers on push to `main` or manual run.
    
2. Builds & tests the app.
    
3. Creates Docker image and pushes to **Amazon ECR**.
    
4. Updates the Kubernetes deployment on **EKS**.
    
5. Monitors rollout status — fails pipeline if deploy fails.
    

---

## 💡 **Best Practices**

- Use **`workflow_dispatch`** for manual controlled releases.
    
- Add **`matrix build`** for multi-language microservices.
    
- Store AWS/EKS configs in a separate **Infra repo**.
    
- Integrate with **ArgoCD** for GitOps-style continuous deployment.
    

---


> 🎯 Goal: GitHub Actions handles **build & image push**,  
> while **ArgoCD automatically detects changes** in your Git repo and **deploys to EKS**.

---

# ⚙️ **GitHub Actions + ArgoCD (GitOps Pipeline)**

📁 **File:** `.github/workflows/gitops-cicd.yml`

```
name: GitOps CI/CD Pipeline

on:
  push:
    branches: [ main ]
  workflow_dispatch:

env:
  AWS_REGION: ap-south-1
  ECR_REPO: myapp-repo
  IMAGE_TAG: ${{ github.sha }}
  MANIFEST_REPO: my-org/myapp-manifests
  DEPLOYMENT_FILE: k8s/deployment.yaml

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      # 🧾 Step 1: Checkout app source
      - name: Checkout application source
        uses: actions/checkout@v4

      # 🧱 Step 2: Setup Node.js (example)
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      # 📦 Step 3: Install and test
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test

      # 🔐 Step 4: Configure AWS credentials
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ env.AWS_REGION }}

      # 🐳 Step 5: Login to Amazon ECR
      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      # 🐳 Step 6: Build and Push Docker image
      - name: Build and push Docker image
        run: |
          IMAGE_URI=${{ steps.login-ecr.outputs.registry }}/${{ env.ECR_REPO }}:${{ env.IMAGE_TAG }}
          docker build -t $IMAGE_URI .
          docker push $IMAGE_URI
          echo "IMAGE_URI=$IMAGE_URI" >> $GITHUB_ENV

  update-manifests:
    needs: build-and-push
    runs-on: ubuntu-latest

    steps:
      # 🧾 Step 1: Checkout the manifest repository
      - name: Checkout manifests repo
        uses: actions/checkout@v4
        with:
          repository: ${{ env.MANIFEST_REPO }}
          token: ${{ secrets.GITHUB_TOKEN }}

      # 🛠️ Step 2: Update deployment manifest image
      - name: Update image tag in manifest
        run: |
          sed -i "s|image: .*|image: $IMAGE_URI|g" ${{ env.DEPLOYMENT_FILE }}

      # 💾 Step 3: Commit and push manifest changes
      - name: Commit and push changes
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "actions@github.com"
          git add ${{ env.DEPLOYMENT_FILE }}
          git commit -m "Update image to $IMAGE_URI"
          git push
```

---

## 🧩 **Flow Explanation**

1. **Code Repo (App Source)** → triggers workflow on push.
    
2. Builds app → pushes image to **Amazon ECR**.
    
3. Updates **Kubernetes manifest repo** with the new image tag.
    
4. **ArgoCD** watches the manifest repo → detects change → deploys automatically to **EKS**.
    

---

## 📘 **Setup Requirements**

### 1️⃣ **App Repo (this pipeline)**

- Contains your app source code
    
- `.github/workflows/gitops-cicd.yml`
    

### 2️⃣ **Manifest Repo**

Example folder structure:

```
k8s/
 ├── deployment.yaml
 ├── service.yaml
 └── ingress.yaml
```

Inside `deployment.yaml`:
```
containers:
  - name: myapp
    image: <ECR_REPO>:<TAG>
```

### 3️⃣ **ArgoCD**

- Connect ArgoCD to **manifest repo** (not the app repo).
    
- Configure **auto-sync**:
```
argocd app set myapp --sync-policy automated --auto-prune --self-heal
```

---

## 🔐 **Secrets Required**

|Secret Name|Description|
|---|---|
|`AWS_ACCESS_KEY_ID`|IAM user key|
|`AWS_SECRET_ACCESS_KEY`|IAM secret|
|_(Optional)_ `GH_PAT`|GitHub Personal Access Token (if private repo access needed)|
## 💡 **Why This Is Ideal**

- GitHub Actions only handles build + image push.
    
- ArgoCD handles deployment — **no kubectl needed** in pipeline.
    
- Ensures full **GitOps compliance** (Infra state = Git state).
    
- Enables **auditability** and **automatic rollback** via Git.