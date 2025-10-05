
## 🚀 What is IAM?

**IAM (Identity and Access Management)** is an AWS service used to **securely control access** to AWS resources.  
It helps decide:

- **Who** can access (identity: user/role)
- **What** they can do (policy: permissions)
- **Where/when** they can do it

👉 Think of IAM like the **security guard** of AWS — it checks the ID (user/role) and allows/denies entry based on the rules (policy).

---

## 🧑‍💻 IAM User
- Represents a **person** (developer, admin, tester).
- Has **long-term credentials** (username, password, access keys).
- Example: A developer who needs to log in to AWS console.
👉 _Analogy: An employee with their own office key._

---
## 🎭 IAM Role
- Represents a **temporary identity** that AWS services or users can assume.
- Provides **temporary credentials**.
- Commonly used by **EC2, Lambda, or cross-account access**.
- Example: An EC2 instance assumes a role to read/write from S3.
👉 _Analogy: A visitor badge — you wear it temporarily to access certain areas._
---
## 📜 IAM Policy
- A **JSON document** that defines permissions (Allow/Deny).
- Attached to a **user, group, or role**.
- Example: A policy that allows `s3:PutObject` only in a specific bucket.
👉 _Analogy: The rulebook the security guard follows — “This person can only enter the server room, not the finance office.”_
---
### 🔑 Easy way to remember: **U-R-P (User, Role, Policy)**
- **User → Person**
- **Role → Temporary access**
- **Policy → Permissions (rulebook)**
---

##### **How do you implement cross-account access in AWS?**
**Answer:**  
Use **IAM roles with trust policies**.
- In Account A (resource account): Create a role with necessary permissions.
- In Account B (user account): Allow users/groups to assume the role.
- Use **STS (Security Token Service)** `assume-role` API to get temporary credentials.