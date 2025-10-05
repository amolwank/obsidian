## **What is SSM Parameter Store?**

- It’s a **secure, scalable storage** for configuration data and secrets.
    
- You can store values like:
    
    - DB connection strings
        
    - API keys
        
    - Passwords
        
    - App configurations
        
- Part of **AWS Systems Manager** service.
    

---

## **Key Features**

1. **Secure Storage**
    
    - Supports plain text and **encrypted values** using AWS KMS.
        
2. **Hierarchical Organization**
    
    - Store parameters in a tree structure (`/app/dev/db/password`).
        
3. **Versioning**
    
    - Each update creates a new version, so you can roll back.
        
4. **Access Control**
    
    - Use **IAM policies** to control who/what can read/write.
        
5. **Integration**
    
    - Works with **EC2, ECS, Lambda, EKS**, and CI/CD pipelines.
        
    - Example: Your app retrieves DB credentials from Parameter Store at runtime.
        
6. **Auditing**
    
    - AWS CloudTrail logs all access to parameters.
        

---

## **Types of Parameters**

- **Standard Parameters** → free, up to 4 KB in size.
    
- **Advanced Parameters** → larger size, higher throughput, features like policies.
    

---

## **Common Use Cases**

- Store **environment variables** for applications.
    
- Manage **secrets** (passwords, tokens) without hardcoding.
    
- Pass configs securely into **Lambda functions or ECS tasks**.
    
- Enforce compliance by controlling sensitive info via IAM.


## **Interview-Ready Answer**

_"AWS SSM Parameter Store is a secure key-value store for configuration and secrets. In one of my projects, we used it to store database passwords and API keys instead of hardcoding them in code or environment files. Applications retrieved these values at runtime with IAM permissions. We also encrypted sensitive parameters with KMS and used versioning for rollbacks. This improved security, centralized configuration management, and simplified secret rotation."_

---