# ⚡ Caching & CDN (Content Delivery Network)

---

## 🔸 What is Caching?

**Caching** stores frequently accessed data in a **local or nearby memory** to reduce latency and speed up access.

It helps avoid fetching the same data repeatedly from slower sources like databases or remote servers.

---

## 🧱 Where is Cache Placed?

- 📌 **In Server Memory** — fast access for APIs or backend systems  
- 📌 **In Database Layer** — commonly used with tools like Redis or Memcached  
- 📌 **Client-side** — browser caches, local storage

---

## 🧠 Common Caching Problems

1. **Write Consistency** – How to ensure cache reflects updated data  
2. **Eviction Strategy** – What data to remove when the cache is full  
3. **Cache Misses** – What if the requested data isn’t in the cache?

These are handled by setting a proper **cache policy**.

---

## 🛠️ Caching Strategies

- **LRU (Least Recently Used)** – Remove data that hasn’t been used recently  
- **LFU (Least Frequently Used)** – Remove data used the least number of times  

> These help balance performance and memory limits.

---

## 🚫 Trashing

**Trashing** happens when:

- Data is evicted or updated too frequently  
- Useful data is removed unnecessarily  
- This increases latency and wastes resources

---

## 🕓 Eventual Consistency in Caching

Sometimes, cache is not updated instantly.

- Cached data is refreshed **periodically**  
- In between, users may see **stale data**
- This is known as **eventual consistency**

Trade-off between **freshness** and **performance**

---

## 🛡️ Avoiding Single Point of Failure

To make caching reliable:

- Use **multiple servers or nodes**
- Add **backup replicas** (e.g., Master-Slave architecture)
- Use **multiple gateways** with DNS-based load balancing
- Deploy across **multiple regions**

> Note: These techniques increase reliability but also **increase cost**.

---

## 🌐 What is a CDN?

**CDN (Content Delivery Network)** is a geographically distributed caching system that stores **static or heavy content** (e.g., images, videos, scripts) closer to users.

---

## ⚙️ How CDN Works

- Stores content in **edge servers** near the user
- Reduces **latency** and improves **load time**
- Helps with **regional regulation** and data compliance

---

## 🧪 Real-World CDN Examples

- **Amazon CloudFront** – Global CDN integrated with AWS  
- **Netflix** – Uses **Chaos Monkey** (a tool that randomly shuts down servers) to test system resilience  
- **Cloudflare, Akamai** – Popular CDN providers

---

## ✅ Benefits of CDN

- Faster content delivery  
- Offloads traffic from origin server  
- Reduces latency  
- Helps handle large volumes of users globally

---

## 🔚 Summary

| Feature                  | Caching                          | CDN                            |
|--------------------------|----------------------------------|---------------------------------|
| Purpose                  | Store frequently used data       | Deliver content closer to users |
| Speed                    | High (microseconds)              | High (low latency globally)     |
| Data Type                | Dynamic (API, DB)                | Static (images, video, scripts) |
| Placement                | Server, DB, client               | Edge nodes (global)             |
| Popular Tools            | Redis, Memcached                 | CloudFront, Cloudflare          |

---

> 🎯 **Caching** and **CDNs** are essential for building fast, scalable, and reliable systems in modern applications.
