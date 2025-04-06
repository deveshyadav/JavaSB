📌 Equivalent names in popular architectures:
Layering Style	Equivalent
Clean Architecture	Domain → App → Infra
Hexagonal Architecture	Domain ↔ Ports ↔ Adapters
Onion Architecture	Core (Domain) → App → Infra
DDD Modular Monolith	Domain modules + application services + external adapters


# 🧠 5. Failure Handling – Kafka, Mongo, Consumers

## 🔹 A. Kafka Goes Down

1.  **Kafka Replication (min ISR)**
    * Kafka stores each topic's data across multiple replicas (brokers).
    * **ISR (In-Sync Replicas):** replicas that have fully caught up with the leader.
    * **min.insync.replicas:** the minimum number of replicas that must be available for Kafka to accept writes.

    ```yaml
    # Example Kafka config
    min.insync.replicas = 2
    acks = all
    ```

    💡 If a producer sends a message and fewer than 2 replicas are alive, Kafka rejects the write.

    This ensures durability even if a broker dies right after a write.

2.  **Producer Retry with Exponential Backoff**
    * Kafka producers can auto-retry sending if Kafka is unavailable.
    * Use exponential backoff to avoid flooding:

    ```java
    retries = 5
    retry.backoff.ms = 100  // Try after 100ms, then 200ms, then 400ms...
    ```

    This prevents crashing on transient outages.

3.  **Disk-Based Buffer (Optional)**
    * If producer cannot send data to Kafka (e.g., network issue), it can:
        * Write to a local buffer (e.g., disk) temporarily.
        * A background thread later flushes this to Kafka.

    💡 Helps avoid data loss if Kafka is down and you don’t want to block your main service.

## 🔹 B. MongoDB Slows Down

1.  **Sharding + Replica Sets**
    * **Sharding:** spreads write/read load across nodes.
    * **Replica Sets:** ensure redundancy + failover.
    * Use hash-based sharding on `shipmentId` to spread writes.

2.  **Write Concern**
    * `w=1`: ack from primary node only.
    * `w=majority`: ack from primary + majority of replicas.

    ```java
    collection.withWriteConcern(WriteConcern.MAJORITY).insertOne(doc);
    ```

    💡 Use `w=1` for low latency, `w=majority` for high durability.

    If Mongo is slow, reduce write concern temporarily.

3.  **Bulk Writes & Throttling**
    * Instead of inserting 1 document at a time → batch them:

    ```java
    collection.insertMany(batchDocs);
    ```

    * Add throttling to limit number of writes/sec:
        * e.g., max 1000 writes/sec per instance.

    💡 Use a queue or buffer if you hit DB rate limits.

## 🔹 C. Consumer Crashes Mid-Processing

Kafka Consumer Model:

* Consumer polls messages from a topic.
* Processes the message.
* Commits offset (manual or auto).

If crash occurs before offset is committed, on restart:

* Kafka re-delivers from the last committed offset.
* You get **duplicate message processing risk**.

**To Avoid Issues:**

✅ **Enable manual offset commit:**

```java
consumer.commitSync();  // Only commit after successful processing

```java



# 🧠 Kafka – Key Concepts & Deep Insights

---

## 🔹 Core Kafka Components

| Term        | Definition |
|-------------|------------|
| **Broker**  | A Kafka server that stores and serves topic data (messages). |
| **Topic**   | A logical category to which messages are published (like a folder). |
| **Partition** | A subdivision of a topic — an append-only log storing ordered messages. |
| **Replica** | A copy of a partition stored on another broker for high availability. |
| **Leader**  | The main replica of a partition that handles all reads/writes. |
| **Follower** | A backup replica that replicates from the leader but doesn't serve clients. |
| **ISR (In-Sync Replicas)** | Set of replicas fully caught up with the leader and eligible for leadership. |

---

## 🔹 Kafka Partitioning & Load Balancing

- **Messages are distributed across partitions** (via round-robin or key hashing).
- **Kafka guarantees order only within a partition.**
- To preserve order (e.g., all events for a shipment), use the same **key** to ensure messages land in the same partition.

---

## 🔹 Consumer Group Behavior

- **Only one consumer per partition in a group** at a time.
- Consumers in a group divide partitions exclusively.
- More consumers than partitions → extra consumers stay idle.
- Message order is preserved within a partition.

---

## 🔹 Replication Factor & Brokers

- **Replication Factor = 1** → Only one copy, no failover.
- **Replication Factor > 1** → Kafka creates followers on other brokers.
- You can have many brokers, even with one partition — but only one will be used if replication = 1.

---

## 🔹 Offsets & Message Processing

- **Offset**: Points to where the consumer left off in a partition.
- **Auto Commit**: Kafka commits offsets in background → risk of data loss on crash.
- **Manual Commit**: Safer; commit offset only after processing is successful.
- **Crash before commit = reprocessing on restart** (risk of duplication unless handler is idempotent).

---

## 🔹 Retry & DLQ Patterns

- Retry failed messages with **exponential backoff**.
- After N retries, send to a **Dead Letter Queue (DLQ)** — a separate Kafka topic.
- Allows system to skip "poison messages" and proceed with rest.

---

## 🔹 Circuit Breaker & Resilience

- Use **Resilience4j** or **Hystrix** in Java to trip breakers on repeated failures.
- Prevents retry storms and cascading failures.
- Can be combined with retry + DLQ for robust failure handling.

---

## 🔹 Performance Considerations

| Metric | Formula |
|--------|---------|
| Throughput | Events/sec = total events ÷ time window |
| Bandwidth | Events/sec × event size |
| Storage/day | Events × payload size |
| Caching | Cache latest shipment location in Redis; not full shipment data |

---

## 🔹 Kafka Best Practices Summary

- Use **manual offset commit + idempotent processing**.
- Use **partition key** to preserve order (e.g., shipmentId).
- **Never assign same partition to multiple consumers in a group.**
- **Enable replication** in production for failover and durability.
- Use **DLQ + observability tools (Prometheus, Grafana)** for resilient ops.


