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
