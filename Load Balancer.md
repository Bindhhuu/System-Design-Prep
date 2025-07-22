# 🔁 Consistent Hashing

Consistent hashing is a smart way to distribute data or requests across multiple servers in a **balanced** and **efficient** way, especially in distributed systems.

---

## 🧠 What is Hashing?

Hashing uses a function to convert a request or key into a number.  
This number helps decide **which server** will handle the request.

Example:  
If you have `n = 4` servers and a request with `id = 35`,  
you can hash it as:

h(35) = hash(35) % 4


The result tells which of the 4 servers will handle the request.

---

## 🌀 The Problem

When you **add or remove servers**, this kind of hashing changes drastically — many request-to-server mappings break.  
This causes data or cache to be **reassigned all over**, increasing system load and reducing performance.

---

## 🔄 Why Consistent Hashing?

Consistent hashing **solves this problem** by:

- Placing all servers and requests on a **circular ring** (hash ring)
- Mapping both servers and requests using the same hash function
- Sending each request to the **next server in the clockwise direction**

This ensures that **only a few requests change servers** when servers are added or removed.

---

## 📌 Benefits

### ✅ Caching Efficiency
If certain requests always go to the **same server**, the data can be **cached** on that server for faster response.

### ✅ Smooth Scaling
When a server is added or removed:
- Only a **small number of keys** need to be moved
- Most of the system remains **unchanged**

---

## 📊 Load Distribution

If:
- `x` = number of requests  
- `n` = number of servers  

Then each server ideally handles about: x / n requests


This balances the system and avoids overloading.

---

## 🛠️ Real-World Use Cases

- Distributed caches (e.g., Memcached, Redis)
- NoSQL databases (e.g., Cassandra, DynamoDB)
- Scalable load balancers

---

## 🔍 Summary

| Feature                 | Without Consistent Hashing | With Consistent Hashing   |
|------------------------|----------------------------|----------------------------|
| Server Add/Remove      | Many keys remapped         | Few keys remapped          |
| Cache Efficiency       | Poor                       | High (same request = same server) |
| Scalability            | Low                        | High                       |
| Load Balancing         | Average                    | Smooth and predictable     |

---

> 🚀 Consistent hashing keeps distributed systems fast, stable, and scalable — even as they grow or change.


