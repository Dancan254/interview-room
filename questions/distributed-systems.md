# Distributed Systems

### Why retrying a payment can charge the card twice
- **Category:** Distributed Systems / Idempotency
- **Level:** Senior
- **Languages:** Any
- **Status:** Scripted
- **Video:** -

**Answer (draft):**

Network timeouts break the illusion of exactly-once execution. The server may have processed the first attempt; you just never saw the response. Retrying without an idempotency key re-executes the operation.

Fix: the client generates a unique idempotency key per logical operation. The server stores the key with the result before responding. A retry with the same key returns the stored result instead of re-executing.

```java
@PostMapping("/payments")
public ResponseEntity<?> pay(@RequestHeader("Idempotency-Key") String key,
                             @RequestBody PaymentRequest req) {
    // check Redis for existing result
    PaymentResult cached = redis.get(key);
    if (cached != null) return ResponseEntity.ok(cached);

    PaymentResult result = paymentService.charge(req);
    redis.setex(key, 86400, result);  // 24h TTL
    return ResponseEntity.ok(result);
}
```

### Your Kafka consumer crashes after processing but before committing the offset
- **Category:** Distributed Systems / Messaging
- **Level:** Senior
- **Languages:** Java
- **Status:** Scripted
- **Video:** -

**Answer (draft):**

The offset is still the old value, so the consumer re-reads the message on restart. Kafka gives you **at-least-once delivery** by default. Your consumer must be idempotent or deduplicate on the event ID.

```java
@KafkaListener(topics = "payments")
public void onPayment(PaymentEvent event) {
    if (redis.setnx("processed:" + event.getId(), "1", Duration.ofHours(1))) {
        processPayment(event);  // only if not seen before
    }
}
```

### Two application instances run the same scheduled job at midnight. How do you prevent duplicate work?
- **Category:** Distributed Systems / Coordination
- **Level:** Mid
- **Languages:** Any
- **Status:** Planned
- **Video:** -

### How do you update the database and publish a Kafka event without losing one of them?
- **Category:** Distributed Systems / Transactional Outbox
- **Level:** Senior
- **Languages:** Any
- **Status:** Planned
- **Video:** -

### One dependency slows down and your retries take down the whole system. What went wrong?
- **Category:** Distributed Systems / Resilience
- **Level:** Senior
- **Languages:** Any
- **Status:** Planned
- **Video:** -

### How do you preserve event order for one customer while processing different customers in parallel?
- **Category:** Distributed Systems / Messaging
- **Level:** Mid
- **Languages:** Any (answer with Kafka)
- **Status:** Planned
- **Video:** -

### Your distributed lock expires while the worker is still running. What protects the shared resource now?
- **Category:** Distributed Systems / Distributed Locks
- **Level:** Senior
- **Languages:** Any
- **Status:** Planned
- **Video:** -
