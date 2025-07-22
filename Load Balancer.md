# ⚖️ Load Balancing

Load balancing is the process of distributing incoming network traffic across multiple servers to ensure no single server becomes overwhelmed.

---

## 🔧 Why Load Balancing?

- Prevents **overloading** of any single server
- Improves **performance** and **availability**
- Ensures **fault tolerance** and **redundancy**
- Enables **horizontal scaling**

---

## 🧰 Types of Load Balancers

1. **Layer 4 (Transport Layer)**  
   - Operates at TCP/UDP level  
   - Example: AWS Network Load Balancer

2. **Layer 7 (Application Layer)**  
   - Works with HTTP/HTTPS traffic  
   - Can make decisions based on URL, cookies, headers  
   - Example: NGINX, AWS Application Load Balancer

---

## 🛠️ Load Balancing Algorithms

- **Round Robin** – Sends requests to servers in order  
- **Least Connections** – Sends to the server with fewest active connections  
- **IP Hashing** – Maps user IP to a specific server  
- **Random** – Randomly selects a server  

---

## 🧱 Examples in Real Life

- NGINX, HAProxy  
- AWS ELB (Elastic Load Balancer)  
- Cloudflare Load Balancer  

---

## ✅ Advantages

- Better resource utilization  
- High availability  
- Easy to scale horizontally  

## ❌ Disadvantages

- Adds some latency  
- Can be a single point of failure (unless redundant)  

---

> Tip: Always use health checks with load balancers to route traffic away from unhealthy servers.

# 🔁 Consistent Hashing

Consistent Hashing is a technique to evenly distribute data across nodes in a **scalable and fault-tolerant** way.

---

## 🧠 Why Use It?

- Handles **dynamic scaling** (adding/removing servers) smoothly  
- Minimizes **data movement** when nodes change  
- Used in **distributed systems**, **caches**, and **databases**

---

## 🔄 How It Works

1. Hash the servers and place them on a **ring**  
2. Hash the data and place it on the ring  
3. Each data item goes to the **next clockwise server** on the ring  

---

## 🔧 Example

- Servers A, B, C are placed on a hash ring  
- A new key is hashed and placed on the ring  
- It goes to the next server in clockwise direction  

If server B is removed, only the keys that were on B move to the next server — not all keys!

---

## 🛠 Applications

- Distributed Caching (e.g., Memcached, Redis clusters)  
- NoSQL Databases (e.g., Cassandra, DynamoDB)  
- Load balancing strategies in distributed environments  

---

## ✅ Advantages

- Scalable  
- Efficient with minimal disruption  
- Great for dynamic environments  

## ❌ Disadvantages

- Implementation can be complex  
- Requires a good hash function for even distribution  

---

> Consistent hashing is a key design pattern behind resilient, scalable distributed systems.
