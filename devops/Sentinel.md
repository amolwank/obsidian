## **What is Sentinel?**

- **Sentinel** is a **policy-as-code framework** created by HashiCorp.
    
- It’s used to enforce **fine-grained, logic-based policies** in HashiCorp tools like **Terraform, Vault, Nomad, and Consul**.
    
- Think of it as a way to write rules that control **how infrastructure is provisioned or managed**.
    

---

## **Why It’s Useful**

- Helps enforce **compliance, security, and governance** in infrastructure as code (IaC).
    
- Prevents misconfigurations before they reach production.
    
- Example: You can write a Sentinel policy that **denies creation of any AWS EC2 instance larger than `t2.medium`** in a dev environment.
    

---

## **How It Works**

1. **Define Policies**
    
    - Written in the **Sentinel language** (similar to HCL/JSON).
        
2. **Attach to Workflows**
    
    - Integrated with Terraform Enterprise/Cloud, Vault, Nomad, etc.
        
3. **Enforcement Levels**
    
    - **Advisory** → Warn only.
        
    - **Soft Mandatory** → Can override with approval.
        
    - **Hard Mandatory** → Blocks the run completely.
        

---

## **Example Sentinel Policy (Terraform)**

```
# Only allow t2.micro and t2.small instance types
import "tfplan"

main = rule {
  all tfplan.resources.aws_instance as _, instances {
    all instances as _, instance {
      instance.applied.instance_type in ["t2.micro", "t2.small"]
    }
  }
}
```
👉 This policy ensures no one can provision expensive instance types accidentally.

---

## **Interview-Ready Summary**

_"Sentinel is a policy-as-code framework by HashiCorp that lets us enforce governance and compliance in tools like Terraform. It works by defining policies that check infrastructure plans before they are applied. For example, we used Sentinel in Terraform Cloud to restrict EC2 instance sizes in dev accounts and enforce mandatory tagging. This ensured cost control and security compliance across all environments."_

---