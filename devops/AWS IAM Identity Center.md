AWS IAM Identity Center (formerly **AWS Single Sign-On / AWS SSO**) is a service that allows you to **centrally manage access to multiple AWS accounts and business applications** for users without creating individual IAM users in each account.

Here’s a detailed breakdown:

---
## **1. Purpose**
- Simplifies **user access management** across multiple AWS accounts and cloud apps.
- Eliminates the need to create separate IAM users for each person.
- Provides **Single Sign-On (SSO)** so users can log in once and access all assigned accounts/apps.
---

## **2. Key Features**

1. **Centralized User Management**
    
    - Integrates with **AWS Managed Users** or external identity providers (IdP) via SAML 2.0, such as **Microsoft AD, Okta, Azure AD**.
        
2. **Single Sign-On**
    
    - Users log in once and access multiple AWS accounts or business apps (Salesforce, GitHub, etc.) without re-entering credentials.
        
3. **Permission Sets**
    
    - Instead of attaching IAM policies to each user, IAM Identity Center uses **permission sets** (a set of IAM policies).
        
    - Assign permission sets to users or groups in specific AWS accounts.
        
4. **Cross-Account Access**
    
    - Users can assume IAM roles automatically in different AWS accounts using assigned permission sets.
        
5. **Audit & Compliance**
    
    - All logins and role assumptions can be tracked in **CloudTrail**.
        
    - Simplifies security audits because users don’t have multiple IAM accounts.
        

---

## **3. How It Works (High-Level Flow)**

1. **User logs in** to the AWS IAM Identity Center portal (web or corporate IdP).
    
2. **SSO authenticates** the user using credentials from AWS Identity Store or external IdP.
    
3. IAM Identity Center determines which **AWS accounts and permission sets** the user has access to.
    
4. User clicks on the account → IAM Identity Center issues **temporary STS credentials** to assume the corresponding IAM role in that account.
    
5. User can now access AWS resources **without having a dedicated IAM user**.
    

---

## **4. Benefits**

- Centralized control over **hundreds or thousands of users**.
    
- **Least privilege** enforced using permission sets.
    
- No long-lived IAM user credentials → reduces security risks.
    
- Integrates with **existing corporate directory** for seamless onboarding/offboarding.
    

---

## **5. Use Case Example**

> A company has 10 AWS accounts and 200 developers. Instead of creating 200 IAM users in each account:
> 
> - Integrate with AWS IAM Identity Center.
>     
> - Developers log in via corporate credentials.
>     
> - Assign them permission sets (e.g., `DeveloperAccess`, `ReadOnly`).
>     
> - Developers can switch accounts in a single portal without separate passwords.
>     

---

