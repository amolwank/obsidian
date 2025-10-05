Here are the key ways to secure CloudFront:

---

### 🔹 **1. Restrict Access to Origin**

- Use **Origin Access Identity (OAI)** for S3 → only CloudFront can access the S3 bucket, not the public.
    
- Or use **Origin Access Control (OAC)** (newer, recommended) → adds tighter control with signed requests.
    

---

### 🔹 **2. HTTPS Everywhere**

- Enforce **HTTPS between viewer ↔ CloudFront** and **CloudFront ↔ Origin**.
    
- Configure **viewer protocol policy = Redirect HTTP to HTTPS**.
    

---

### 🔹 **3. Use WAF & Shield**

- **AWS WAF** → Protects against SQL injection, XSS, malicious requests.
    
- **AWS Shield Standard/Advanced** → Protects against DDoS attacks.
    

---

### 🔹 **4. Signed URLs & Signed Cookies**

- Use **signed URLs/cookies** for premium/private content.
    
- Only authorized users get access, with expiry times.
    

---

### 🔹 **5. Geo Restriction**

- Block or allow content delivery based on country.
    
- Useful for compliance or licensing restrictions.
    

---

### 🔹 **6. Cache & Header Controls**

- Add **custom headers** between CloudFront and Origin to verify requests.
    
- Use **cache policy & response headers policy** to prevent sensitive data leaks.
    

---

### 🔹 **7. Logging & Monitoring**

- Enable **CloudFront access logs** in S3.
    
- Monitor with **CloudWatch metrics & alarms**.
    
- Use **AWS CloudTrail** for auditing API calls.
    

---

### 🔹 **8. Integration with Cognito / IAM**

- Use **Cognito or IAM roles** with signed requests for authenticated access.
    

---

✅ **In Short (Interview one-liner):**  
“To secure CloudFront, I restrict origin access with OAI/OAC, enforce HTTPS, use WAF & Shield for protection, implement signed URLs/cookies for private content, apply geo restrictions, and enable logging with CloudWatch and CloudTrail for monitoring.”