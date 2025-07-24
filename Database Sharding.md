# 🧩 Sharding in Databases

**Sharding** is the process of **partitioning a large database into smaller, manageable pieces** called *shards*.

Each shard holds a portion of the data and can be stored on a separate server or database instance.

---

## 🎯 Why Use Sharding?

- ✅ Improves **scalability** of large systems
- ✅ Increases **performance** by reducing load on a single DB
- ✅ Decreases **query time** by spreading data
- ✅ Maintains **consistency** in large-scale architectures

---

## 🧰 Sharding Strategies

### 1. 🔢 Hash-Based Sharding
- Data is partitioned using a **hash function** on a key (e.g., `user_id`)
- Ensures **even distribution** of data
- Hard to perform range queries

### 2. 🔢 Range-Based Sharding
- Data is partitioned by a **range of values** (e.g., users A–F in Shard 1, G–Z in Shard 2)
- Easy for **range queries**, but risk of uneven data distribution

---

## 🛠️ Best Practices

- ✅ Create indexes for faster lookups
- ✅ Use **Master-Slave architecture**:  
  - Writes go to the master  
  - Reads can be handled by replicas (slaves)
- ✅ Define a good shard key (frequently queried, evenly distributed)

---

## ⚠️ Common Issues

### ❌ Cross-Shard Joins
- Joins across shards are complex and expensive  
- Often require **two or more queries**

### ❌ No Dynamic Partitioning
- Hard to add or remove shards dynamically  
- Manual rebalancing often needed

---

## 📌 Summary

| Feature              | Benefit                                |
|----------------------|----------------------------------------|
| Performance          | Reduces query load                     |
| Scalability          | Allows horizontal scaling              |
| Consistency          | Maintains system stability             |
| Complexity           | Requires careful shard key selection   |
| Challenges           | Cross-shard queries, rebalancing       |

---

> 🧠 Sharding is critical in high-scale systems (like Facebook, Amazon) to ensure fast and reliable access to massive datasets.
