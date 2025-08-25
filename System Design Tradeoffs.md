# 🧭 System Design Trade-offs

Quick, interview-ready notes on common trade-offs. Each section explains **what**, **when to choose**, **pitfalls**, and **examples**—clear and precise.

---

## 1) Pull vs. Push

| Aspect | Pull (Consumers fetch) | Push (Producers deliver) |
|---|---|---|
| Control | Consumer-driven polling cadence | Producer/broker-driven delivery |
| Backpressure | Natural (slow consumers pull less) | Must be engineered (buffers, flow control) |
| Latency | Higher (poll interval) | Lower (near real-time) |
| Complexity | Simpler infra; more client logic | More infra features (subscriptions, retries) |
| Fan-out | Harder | Easy (broadcast to many) |

**Choose Pull when:** workloads are bursty, consumers vary in speed, or you need simple reliability (e.g., workers polling a queue).
  
**Choose Push when:** you need low latency, real-time notifications, easy fan-out (e.g., pub-sub topics, webhooks).

**Pitfalls:**  
- Pull: wasted polls, higher average latency.  
- Push: overload consumers without flow control (use ack/retry, rate limits).

**Examples:**  
- Pull: SQS + poller workers, cron-based ETL.  
- Push: Kafka consumers with broker push, Firebase push notifications, webhooks.

---

## 2) Memory vs. Latency

| Use More Memory | Result |
|---|---|
| In-memory caches (Redis, app cache) | Lower read latency |
| Precomputation/materialization | Faster queries |
| Bigger buffers/prefetch | Fewer I/O stalls |

**Choose Memory when:** you need sub-ms reads, repeated access patterns, or hot sets fit in RAM.

**Choose Lower Memory when:** cost-sensitive, very large datasets, or strict memory limits.

**Pitfalls:** cache invalidation, stale data, GC pressure, cold starts.

**Examples:**  
- Hot user profiles in Redis → ms latency.  
- Pre-aggregated analytics tables → quick dashboards.

---

## 3) Throughput vs. Latency

> **Throughput** = work per unit time. **Latency** = time per request.

| Optimize For | Approach |
|---|---|
| Throughput | Batch, compress, queue, async pipelines |
| Latency | Inline processing, smaller payloads, direct paths |

**Choose Throughput when:** bulk processing, analytics, streaming ingestion.

**Choose Latency when:** user-facing interactions, HFT-like paths, SLAs (p95/p99).

**Pitfalls:** batching increases tail latency; per-request sync lowers throughput.

**Examples:**  
- High throughput: Kafka ingestion + batch Spark jobs.  
- Low latency: Search autocomplete with in-memory indices.

---

## 4) Consistency vs. Availability (CAP context)

| Consistency (C) | Availability (A) |
|---|---|
| All nodes see same data after write | System responds even during failures/partitions |
| Strong guarantees, fewer anomalies | May serve slightly stale data |

**CP systems (Consistency + Partition tolerance):** prefer correctness (e.g., relational stores with strict constraints, Zookeeper-like coordination).  
**AP systems (Availability + Partition tolerance):** prefer uptime and eventual consistency (e.g., Dynamo-style KV stores, Cassandra).

**Choose Consistency when:** payments, inventory correctness, ACLs.  
**Choose Availability when:** social feeds, counters, metrics, shopping carts (with reconciliation).

**Pitfalls:** misunderstanding “eventual consistency” behaviors; need idempotency, conflict resolution.

---

## 5) Latency vs. Accuracy

| Lower Latency | Higher Accuracy |
|---|---|
| Approximate/partial results fast | Full, precise results slower |
| Sketches, cached or stale reads | Full recompute, strong reads |

**Choose Low Latency when:** UX requires instant feedback (autocomplete, dashboards), or approximation is acceptable.

**Choose High Accuracy when:** financial statements, compliance, billing.

**Techniques:**  
- Approximate: HyperLogLog, sampling, top-K sketches, cached aggregates.  
- Accurate: transactional reads, full joins/aggregations.

**Pitfalls:** mixing approximations with authoritative flows; failing to mark data as “estimated”.

---

## 6) SQL vs. NoSQL Databases

| Dimension | SQL (Relational) | NoSQL (Non-Relational) |
|---|---|---|
| Schema | Fixed, well-defined | Flexible / schema-less |
| Consistency | Strong (ACID) | Often eventual (BASE) |
| Queries | Rich joins/aggregations | Per-model (docs/KV/column/graph) |
| Scaling | Vertical (read replicas, sharding later) | Horizontal by design |
| Best For | Transactions, relationships | Scale, heterogeneous or large data |

**Choose SQL when:** strong consistency, complex joins, well-structured domain (payments, orders, ERP).

**Choose NoSQL when:** massive scale, high write throughput, flexible schemas, global distribution (feeds, logs, IoT).

**Pitfalls:**  
- SQL: premature complex sharding, slow schema migrations under load.  
- NoSQL: poor data modeling leads to fan-out queries; weak consistency pitfalls.

**Examples:**  
- SQL: PostgreSQL/MySQL for OLTP.  
- NoSQL: Cassandra for time-series; DynamoDB for KV; MongoDB for documents; Neo4j for graphs.

---

## Practical Heuristics (TL;DR)

- **Real-time notify?** → Push; **worker pull** for resilient background jobs.  
- **User-perceived speed?** → Spend **memory** (cache) to drop **latency**.  
- **Batch analytics?** → Favor **throughput**; **interactive UX** → favor **latency**.  
- **Money moves?** → Favor **consistency**; **feeds/metrics** → favor **availability** with reconciliation.  
- **Instant but rough vs. slow but exact?** → Decide **latency vs. accuracy** per endpoint.  
- **Strong relations & ACID?** → SQL; **scale/flexibility?** → NoSQL (pick correct model).

---
