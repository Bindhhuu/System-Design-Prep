# 📈 Vertical and Horizontal Scaling

Understanding the two main ways to scale systems: **Vertical (Scale Up)** and **Horizontal (Scale Out)**.

---

## 🔼 Vertical Scaling (Scale Up)

Increases the capacity of **a single machine** by upgrading its hardware or software.

- ✅ Increases the capacity of individual hardware or software
- ✅ Also known as **scale up**
- ✅ Easy to implement
- ✅ Uses **network calls (RPC)**

### 🧪 Examples
- MySQL  
- Amazon RDS

### ✅ Advantages
- Increases individual capacity
- Easier to manage

### ❌ Disadvantages
- Limited scalability  
- Increases cost significantly  
- **Single point of failure**

---

## 🔁 Horizontal Scaling (Scale Out)

Involves adding more machines (nodes) to distribute traffic and computation.

- ✅ Known as **scale out**
- ✅ Uses **inter-process calls**
- ✅ Better for distributed systems

### 🧪 Examples
- Cassandra  
- MongoDB  
- Google Gmail, YouTube, Yahoo rely heavily on it

### ✅ Advantages
- Increased capacity
- Improved performance
- Increased fault tolerance
- Less prone to single point of failure

### ❌ Disadvantages
- Can be expensive
- More complex infrastructure
- Increased cost and overhead

---

> 🔍 Choosing between vertical and horizontal scaling depends on your system’s requirements, traffic, and fault tolerance needs.

