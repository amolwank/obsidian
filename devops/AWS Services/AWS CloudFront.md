## 🔹 What is CloudFront?
?
- **Amazon CloudFront** is a **Content Delivery Network (CDN)** service.    
- It delivers **web content, videos, APIs, and applications** with **low latency** and **high transfer speed** by caching copies of your content at **edge locations** worldwide.
- Instead of every user fetching data from your origin (like S3 or EC2), CloudFront serves content from the **nearest edge location**.
## 🔹 How CloudFront Integrates with S3

1. **Origin Setup**
    - S3 bucket is configured as the **origin** for CloudFront.
    - CloudFront pulls objects from S3 when requested.
2. **Content Delivery**
    - When a user requests an object (e.g., `image.jpg`), CloudFront checks the nearest **edge cache**.
    - If cached → served instantly.
    - If not cached → CloudFront fetches from S3 → caches at the edge → delivers to user.
3. **Access Control & Security**
    - You can make your **S3 bucket private** and allow access only through CloudFront using **Origin Access Control (OAC)** or older **Origin Access Identity (OAI)**.
    - This prevents direct public access to S3.
4. **Performance Enhancements**
    - Supports **compression, caching policies, signed URLs, and geo-restrictions**.
    - Useful for serving static websites, media files, or software downloads from S3 at scale.
        

---

## 🔹 Example Flow

1. User requests `https://cdn.mysite.com/logo.png`.
2. CloudFront edge location checks cache.
3. If not found → fetches `logo.png` from S3 bucket (origin).
4. Object cached at edge for future requests.
5. User gets faster response, reduced latency.
    

---

✅ **Short Interview-Ready Answer:**  
Amazon CloudFront is a CDN that caches content at edge locations worldwide to reduce latency. It integrates with S3 by using the bucket as an origin, delivering objects securely and efficiently. You can restrict direct bucket access and serve content only through CloudFront using OAC/OAI.

#flashcards 